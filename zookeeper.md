 **使用场景** 
     - 例如某些数据需要动态修改，活动奖品数量 ,开奖时间等一些经常变化的数据等

 **功能** 
     - 统一的后台管理、推送实时生效，支持集群推送

 **使用技术** 
     - springboot
     - zookeepr

   **DEMO** 
      1. 第一步

          ```
<dependency>
   <groupId>com.gitee.levon</groupId>
   <artifactId>idrm-client</artifactId>
   <version>1.0.0-SNAPSHOT</version>
</dependency>
```
     2. 第二步
         ```
ZDrmClient.newInstance("192.168.1.45:2181")
                .setAppName("drm")
                .setScanPackage("org.drm.zdrm.test.resource")
                .build();
```
     3. 第三步
       需要动态修改的数据对象
     ```
@Data
@DRMResource(id = "org.zdrm.test.resource.PrizeRule")
public class PrizeRule {
    @DRMAttribute
    private Integer poolSize = 100;
    @DRMAttribute
    private Boolean poolSwitch = false;
}
```
      5. 第四步
    数据修改后
  ```
PrizeRule prizeRule = ZDrmClient.drm(PrizeRule.class);
System.out.println("获取对象值：" + prizeRule.getPoolSize());
```
