# 使用云市场镜像在弹性伸缩创建ECS实例报错问题 {#concept_s35_r5l_sfb .concept}

使用云市场镜像在弹性伸缩创建 ECS 实例报错问题：Fail to create Instance into scaling group.（The specified image is from the image market. You have not bought it or your quota has been exceeded.）如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40694/154227535230633_zh-CN.jpg)

这个问题是由于当前弹性伸缩服务还不能自动创建镜像市场的第三方镜像，客户需要先到 [云市场](https://market.aliyun.com/software) 购买需要的第三方镜像，购买成功后再回到弹性伸缩服务中创建 ECS 实例即可。

