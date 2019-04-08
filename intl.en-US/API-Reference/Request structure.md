# Request structure {#concept_25927_zh .concept}

This topic introduces the request structure.

## Service address {#section_i24_542_sfb .section}

The following table describes the access endpoints of Auto Scaling API service. To reduce network latency, we recommend that you configure endpoints based on the source from which you call the service.

|Region \(Location\)|Endpoint|
|-------------------|--------|
|Default|ess.aliyuncs.com|
|China \(Qingdao\)|ess.aliyuncs.com|
|China \(Beijing\)|ess.aliyuncs.com|
|China \(Zhangjiakou\)|ess.cn-zhangjiakou.aliyuncs.com|
|China \(Hohhot\)|ess.cn-huhehaote.aliyuncs.com|
|China \(Hangzhou\)|ess.aliyuncs.com|
|China \(Shanghai\)|ess.aliyuncs.com|
|China \(Shenzhen\)|ess.aliyuncs.com|
|Hong Kong|ess.aliyuncs.com|
|Singapore|ess.aliyuncs.com|
|Australia \(Sydney\)|ess.ap-southeast-2.aliyuncs.com|
|Malaysia \(Kuala Lumpur\)|ess.ap-southeast-3.aliyuncs.com|
|Indonesia \(Jakarta\)|ess.ap-southeast-5.aliyuncs.com|
|Japan \(Tokyo\)|ess.ap-northeast-1.aliyuncs.com|
|UK \(London\)|ess.eu-west-1.aliyuncs.com|
|US \(Silicon Valley\)|ess.aliyuncs.com|
|US \(Virginia\)|ess.aliyuncs.com|
|Germany \(Frankfurt\)|ess.eu-central-1.aliyuncs.com|
|UAE \(Dubai\)|ess.me-east-1.aliyuncs.com|
|India \(Mumbai\)|ess.ap-south-1.aliyuncs.com|

## Communication protocols {#section_mh4_w42_sfb .section}

The system supports request communication through the HTTP or HTTPS channel. We recommend that you send requests over HTTPS for enhanced security.

## Request methods {#section_psf_x42_sfb .section}

The system allows you to send HTTP GET requests. This requires request parameters to be included in the request URL.

## Request parameters {#section_alx_x42_sfb .section}

For each request, you must specify the operation you want to execute, namely the Action parameter \(for example, CreateScalingGroup\), and each operation must contain the public and specific request parameters of the specified operation.

## Character encoding {#section_rng_1p2_sfb .section}

Requests and returned results are encoded using the UTF-8 character set.

