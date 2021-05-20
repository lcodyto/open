分布式资源管控
适用场景：
在实际项目中，经常会涉及到一些可变的资源属性，比如：动态开关，一些不常变化的配置等
这类属性通常需要维护在数据库，或者其他缓存、配置文件中
系统功能：
支持动态资源管控，可实现运行时修改系统drm变量，无需重启
业务系统只需引入client包，增加少量代码即可接入
统一的后台管理、推送实时生效，支持集群推送
使用技术：
zookeeper
springboot
使用示例
maven引入

<dependency>
   <groupId>com.gitee.levon</groupId>
   <artifactId>idrm-client</artifactId>
   <version>1.0.0-SNAPSHOT</version>
</dependency>
初始化（也支持spring方式）

ZDrmClient.newInstance("192.168.1.45:2181")
                .setAppName("levon")
                .setScanPackage("org.levon.zdrm.test.resource")
                .build();
需要被管理的对象

@Data
@DRMResource(id = "org.levon.zdrm.test.resource.PrizeRule")
public class PrizeRule {
    @DRMAttribute
    private Integer poolSize = 100;
    @DRMAttribute
    private Boolean poolSwitch = false;
}
测试，poolSize属性支持后台页面实时修改：

PrizeRule prizeRule = ZDrmClient.drm(PrizeRule.class);
System.out.println("获取对象值：" + prizeRule.getPoolSize());

新功能计划表（开发中）
提供idrm-spring-boot-starter，方便springboot项目使用
提供点对点推送，支持针对单个ip地址推送
推送记录查询，支持保存上次推送记录
注：本项目仅供学习交流，由于还在完善中，不建议用于生产环境

后台页面预览
应用配置

环境配置

资源配置

推送管理