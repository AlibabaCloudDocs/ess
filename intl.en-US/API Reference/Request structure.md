# Request structure

This topic describes the request structure used when you call API operations of Auto Scaling.

## Endpoints

To reduce network latency, we recommend that you configure endpoints based on your business location. The following table describes the endpoints of Auto Scaling.

|Region|Public endpoint|VPC endpoint|
|------|---------------|------------|
|Default|ess.aliyuncs.com|None|
|China \(Qingdao\)|ess.aliyuncs.com|ess-vpc.cn-qingdao.aliyuncs.com|
|China \(Beijing\)|ess.aliyuncs.com|ess-vpc.cn-beijing.aliyuncs.com|
|China \(Zhangjiakou\)|ess.cn-zhangjiakou.aliyuncs.com|ess-vpc.cn-zhangjiakou.aliyuncs.com|
|China \(Hohhot\)|ess.cn-huhehaote.aliyuncs.com|ess-vpc.cn-huhehaote.aliyuncs.com|
|China \(Ulanqab\)|ess.cn-wulanchabu.aliyuncs.com|ess-vpc.cn-wulanchabu.aliyuncs.com|
|China \(Hangzhou\)|ess.aliyuncs.com|ess-vpc.cn-hangzhou.aliyuncs.com|
|China \(Shanghai\)|ess.aliyuncs.com|ess-vpc.cn-shanghai.aliyuncs.com|
|China \(Shenzhen\)|ess.aliyuncs.com|ess-vpc.cn-shenzhen.aliyuncs.com|
|China \(Heyuan\)|ess.cn-heyuan.aliyuncs.com|ess-vpc.cn-heyuan.aliyuncs.com|
|China \(Guangzhou\)|ess.cn-guangzhou.aliyuncs.com|ess-vpc.cn-guangzhou.aliyuncs.com|
|China \(Chengdu\)|ess.cn-chengdu.aliyuncs.com|ess-vpc.cn-chengdu.aliyuncs.com|
|China \(Hong Kong\)|ess.aliyuncs.com|ess-vpc.cn-hongkong.aliyuncs.com|
|Singapore \(Singapore\)|ess.aliyuncs.com|ess-vpc.ap-southeast-1.aliyuncs.com|
|Australia \(Sydney\)|ess.ap-southeast-2.aliyuncs.com|ess-vpc.ap-southeast-2.aliyuncs.com|
|Malaysia \(Kuala Lumpur\)|ess.ap-southeast-3.aliyuncs.com|ess-vpc.ap-southeast-3.aliyuncs.com|
|Indonesia \(Jakarta\)|ess.ap-southeast-5.aliyuncs.com|ess-vpc.ap-southeast-5.aliyuncs.com|
|Japan \(Tokyo\)|ess.ap-northeast-1.aliyuncs.com|ess-vpc.ap-northeast-1.aliyuncs.com|
|UK \(London\)|ess.eu-west-1.aliyuncs.com|ess-vpc.eu-west-1.aliyuncs.com|
|US \(Silicon Valley\)|ess.aliyuncs.com|ess-vpc.us-west-1.aliyuncs.com|
|US \(Virginia\)|ess.aliyuncs.com|ess-vpc.us-east-1.aliyuncs.com|
|Germany \(Frankfurt\)|ess.eu-central-1.aliyuncs.com|ess-vpc.eu-central-1.aliyuncs.com|
|UAE \(Dubai\)|ess.me-east-1.aliyuncs.com|ess-vpc.me-east-1.aliyuncs.com|
|India \(Mumbai\)|ess.ap-south-1.aliyuncs.com|ess-vpc.ap-south-1.aliyuncs.com|

## Protocols

You can send requests over HTTP or HTTPS. For a higher level of security, we recommend that you send requests over HTTPS.

## Methods

You can send requests by using the HTTP GET method. In an HTTP GET request, the request parameters must be included in the request URL.

## Parameters

In each request, you must specify the operation such as CreateScalingGroup that you want to perform by using the Action parameter. You must also specify the common request parameters and operation-specific parameters.

## Encoding

All requests and responses are encoded in UTF-8.

