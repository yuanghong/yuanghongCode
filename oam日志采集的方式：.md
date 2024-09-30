# oam日志采集的方式：

1.日志采集是通过oam微服务采集的，oam只部署在集群中的一台机器上且是随机部署，机器上存放日志的目录/data/logs/fluentd-log/在集群中的每台环境上都有，微服务不能直接从别的机器上的目录中拿文件（但可以从所在节点的目录上取文件，挂载即可），因此需要通过在每台机器上部署nginx，nginx挂载机器上的日志存放目录，oam向nginx发送url请求：http：//ip:port/mount的目录路径（nginx中的目录），就可以拿到机器上的日志文件，这是nginx本身具有的功能，不需要额外的配置。

2.msiptool中的日志采集方式则完全不同；msiptool不是微服务，直接存在于机器上的目录中，且集群中的每台机器上都有msiptool的目录；在进行日志采集时，当前环境调用一个采集自身环境日志目录的脚本和两个采集远端环境的日志目录的脚本；需要采集的日志文件全路径被放到一个conf文件中，脚本读取conf们就会采集相应的日志文件

# 需要思考的问题：

## 1.nginx是怎么作为微服务部署到集群环境中的？/怎么在集群环境中部署一个微服务？

### 首先准备好集群环境和docker镜像

### 部署配置：

#### 1.编写deployment.yaml文件：定义微服务的部署配置

---
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: nginx-proxy
  namespace: platform
  labels:
    backup: saas
    name: nginx-proxy
    version: 1.0.0
spec:
  template:
    metadata:
      labels:
        name: nginx-proxy
        version: 1.0.0
        app.kubernetes.io/name: nginx-proxy
    spec:
      hostNetwork: true
      volumes:

        - configMap:
            name: nginx-config
                    name: nginx-config
                - hostPath:
            path: /etc/localtime
                    name: localtime
                        - name: fluented-log
                    hostPath:
            path: /data/logs/fluentd-log
                                - name: containerd-etcd-kubelet-message
                    hostPath:
            path: /data/logs/syslog
                                        - name: message-log
                    hostPath:
            path: /var/log
                                    containers:
                                                - name: nginx-proxy
                    #image: cmc.centralrepo.rnd.huawei.com/td_cloudnative/cnp/nginx:1.22.0
                    image: imagerepo.td-tech.com:5001/nginx:1.22.0
                    imagePullPolicy: IfNotPresent
                    command: ['nginx', '-g', 'daemon off;']
                    volumeMounts:
            - mountPath: /etc/nginx/conf.d/
              name: nginx-config
              readOnly: true
            - mountPath: /etc/localtime
              name: localtime        
            - name: fluented-log
              mountPath: /data/logs/fluentd-log
            - name: containerd-etcd-kubelet-message
              mountPath: /data/logs/syslog
            - name: message-log
              mountPath: /data/logs/messages
    selector:
        matchLabels:
            name: nginx-proxy
            version: 1.0.0

#### 2.创建service.yaml文件：定义如何访问微服务

---
apiVersion: v1
kind: Service
metadata:
  name: nginx-proxy
  namespace: platform
  labels:
    backup: saas
    name: nginx-proxy
    version: 1.0.0
spec:
  type: ClusterIP
  ports:
    - port: 8092
      targetPort: http
      protocol: TCP
      name: nginx-proxy
    selector:
        name: nginx-proxy
        version: 1.0.0

#### 3.定义configMap文件：

---
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-config
  namespace: platform
  labels:
    backup: saas
data:
  platform.conf: |-
    limit_conn_zone $binary_remote_addr zone=conn_limit_zone:10m; # 定义共享内存区域
    server {
      listen  8092;
      error_page   500 502 503 504  /50x.html;
  location = /50x.html {
    root   /usr/share/nginx/html/;
  }

  location / {
    autoindex on;
    limit_conn conn_limit_zone 100;
    limit_rate 4m;
    root /;
  }

}    

#### 那nginx是怎么部署到每个node上的呢？

通过deployment.yml中的kind: DaemonSet，这种部署方式会在集群的没一个节点上起一个pod；

kind: Deployment

replicas: 1

可以指定开启的pod数目，并随机分配到集群的节点上，除非指定了亲和性

亲和性分节点亲和性和pod反亲和性：节点亲和性是只有配置了该标签的节点才有开启当前pod的资格

pod反亲和性：是指具有相同标签的pod不能被调度在同一个node上，比如oam副本数为2，为了避免这两个pod都部署在同一个节点，可以指定podantiaffinity   让他们部署在不同机器上

## 2.日志采集的规则：

  日志每隔一小时就会转储一次，生成.gz文件，同时.log文件会将转储过的日志文件清除；

  采集当天的日志：会采集转储的.gz文件+.log文件

  采集过去天的日志：只采集转储的.gz文件

3.configmap是什么?ClusterIP和node port的区别？

`ConfigMap` 是 Kubernetes 用于管理配置数据的对象，项目是用configmap管理微服务的配置信息—conf，然后挂载到容器内；这样做的目的是将配置与应用的镜像分离，使得更新配置不会影响镜像

## 3.cmcenter代码流程梳理

1.在bean层创建mocmeta和parammeta的实体类

```
@Component
@Data
@ToString
@NoArgsConstructor
public class MocMeta {
    private int mocId;
    private String mocName;
    private String mocNameC;
    private String mocNameE;
    private String dbName;
    private String module; // 域名
    private String moduleC;
    private String moduleE;
    //    private String domain; // 域名
    private String accessControl;
    private String group;
    private String groupC;
    private String groupE;
    private String addWarn;
    private String verify;
    private String modifyWarn;
    private String deleteWarn;
    private List<ParameterMeta> params;
}
```

```
@Component
@Data
@ToString
public class ParameterMeta {
    private String name;
    private String desc;
    private String type;
    private String range;
    private String vlist;
    private String constrain;
    private String defaultValue;
    private String mode;// display update NA
    private boolean priKey = false;
    private boolean notNull = false;

    public enum ParamType {
        PARAM_TYPE_STRING, PARAM_TYPE_INT, PARAM_TYPE_DOUBLE, PARAM_TYPE_ENUM, PARAM_TYPE_BIT_SET, PARAM_IP_ADDRESS, PARAM_TYPE_TIME
    }

    ;
}
```

.定义conrtoller：

```
@RestController
@Slf4j
@RequestMapping(MocMetaController.BASE_PREFIX)
public class MocMetaController {
  public。。。
  @GetMapping("/configapi/configinfo")
  @ResponseBody
  public CMCommonResp queryMocMetaList(@RequestParam("page") int pageNum,
                                         @RequestParam("limit") int pageSize,
                                         @RequestParam("db_moc_name") String dbMocName)   {
    
}
```

**@RestController**: 表明这是一个控制器类，处理 HTTP 请求并返回响应体。它是 `@Controller` 和 `@ResponseBody` 的组合，意味着每个方法的返回值都会直接写入 HTTP 响应中。

**@Slf4j**: 是 Lombok 提供的注解，用于自动生成一个名为 `log` 的日志记录器（Logger），可以方便地在代码中记录日志。

**@RequestMapping(MocMetaController.BASE_PREFIX)**: 定义了一个基本的请求映射前缀，所有该控制器的方法的路径都将以 `/cmcenter` 开头。这使得组织和管理 API 路径更加清晰。

**@GetMapping("/configapi/configinfo")**: 指定此方法处理 HTTP GET 请求，并且请求的路径是 `/cmcenter/configapi/configinfo`。这是一个简化的 `@RequestMapping` 注解，用于处理 GET 请求。

**@ResponseBody**: 指示方法的返回值应该直接作为 HTTP 响应体，而不是被视为视图名称。这个注解在 `@RestController` 中已经隐含包含，所以这里可以省略。

**@RequestParam**: 表示将请求参数绑定到方法参数上。在此方法中，`page`, `limit`, 和 `db_moc_name` 的值将从请求的查询字符串中提取。

整体流程是定义MocMetaController类，然后定义查询接口 queryMocMetaList，在接口函数中调用了mocMetaLoader类中的getMocMeta函数，这个函数里首先通过容器挂载的环境中的目录下找到所有的.xml文件，将file的string对象转换成document对象，获取document的根节点，找到根节点中包含"MOC"的元素，这样就去掉了xml文件中多余的部分。接着将mocmeta和parameter单独处理，mocmeta去调用 formMoc函数，将属性值赋给相应的mocmeta对象；parameter处理相对复杂，将moc节点中包含"parameter"的元素挨个遍历，将属性值赋给相应的parammeta对象，add到parameterMetaList，最后通过mocMeta.setParams赋给实体类；这样就查到了表格的列名

调用 commonSearch函数，构建查询语句，调用 jdbcTemplate.queryForList执行sql查询，将结果以列表形式返回，因为数据库中的数据存在枚举值和密码。需要将数据库数据解析成界面可以查看的数据List。

