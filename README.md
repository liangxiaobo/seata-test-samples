# seata-test-samples

# 运行示例
 示例是根据[官方示例中springcloud-eureka-seata](https://github.com/seata/seata-samples)测试
 
 ## 1.1 下载seata-server
   https://github.com/seata/seata/releases
 
 ## 1.2 运行seata-server
 解压后，修改文件file.conf 中的store.mode="db" 默认为file
 ```json
## transaction log store
store {
  ## store mode: file、db
  mode = "db"

  ## file store
  file {
    dir = "sessionStore"

    ......
  }

  ## database store
  db {
    ......
  }
}

```
修改registry.conf registry中的type="eureka",serviceUrl=你实际的eureka-server地址(本机可写127.0.0.1)，
```json
registry {
  # file 、nacos 、eureka、redis、zk、consul、etcd3、sofa
  type = "eureka"

  nacos {
    serverAddr = "localhost"
    namespace = "public"
    cluster = "default"
  }
  eureka {
    serviceUrl = "http://127.0.0.1:8761/eureka"
    application = "default"
    weight = "1"
  }
}
```

```xml
spring.cloud.alibaba.seata.tx-service-group=my_test_tx_group
```

以上修改完可运行bin目录下的 seata-server.sh
```bash
sh seata-server.sh
```

## 2.1 修改springboot项目中的配置
修改registry.conf中的type="eureka"，application和上面的相同
```json
registry {
  # file 、nacos 、eureka、redis、zk
  type = "eureka"

  eureka {
    serviceUrl = "http://127.0.0.1:8761/eureka"
    application = "default"
    weight = "1"
  }
}
```

