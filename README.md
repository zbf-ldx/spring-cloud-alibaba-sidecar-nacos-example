#使用说明
- 添加依赖
```
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-sidecar</artifactId>
</dependency>
```
- 配置sidecar
```
sidecar:
  #第三方服务地址
  ip: 172.16.3.185
  port: 8080
  #第三方服务健康检查地址，需返回{"status":"UP"}
  health-check-url: http://172.16.3.185:8080/healthy
  health-check-interval: 30000
```

- 启动第三方服务，有接口如下
``` 
@RestController
public class CigarController {


    @GetMapping("/healthy")
    public String healthy() {
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("status","UP");
        return jsonObject.toJSONString();
    }

    @GetMapping("/sidecar")
    public String test() {
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("status","UP");
        jsonObject.put("message","success");
        return jsonObject.toJSONString();
    }
}
```
- 访问： http://localhost:9021/sidecar-service/sidecar
``` 
{"status":"UP","message":"success"}
```