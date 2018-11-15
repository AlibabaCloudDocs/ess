# Signatures {#concept_lfh_xr2_sfb .concept}

This topic introduces the signature.

Auto Scaling performs authentication on each access request. Therefore, each request, whether being sent via HTTP or HTTPS, must contain signature information. By using AccessKeyID and AccessKeySecret, Auto Scaling performs symmetric encryption to authenticate the request sender. The AccessKeyID and AccessKeySecret are officially issued to visitors by Alibaba Cloud \(visitors can apply for and manage them at Alibaba Cloud’s official website\). The AccessKeyID indicates the identity of the visitor. The AccessKeySecret is the secret key used to encrypt and verify the signature string on the server. It must be kept confidential and should only be available to Alibaba Cloud and the user.

When a user calls a server, the following method is used to sign the request:

1.  The Canonicalized Query String is constructed using the request parameters.
    1.  The request parameters are ordered alphabetically by the parameter names \(this includes the "public request parameters" and user-defined parameters for the given request interfaces described in this document, but not the Signature parameter mentioned in "public request parameters"\).

        **Note:** For a request submitted using the GET method, these parameters constitute the parameter section of the request URI \(that is, the section in the URI following "?" and connected by "&"\).

    2.  The name and value of each request parameter are encoded. The names and values must be URL encoded using the UTF-8 character set. The URL encoding rules are as follows:

        -   English letters A–Z and a–z, digits 0–9, and characters "-", "\_", ".", and "~" are not encoded.
        -   Other characters are encoded in the "%XY" format, with "XY" representing the characters’ ASCII code in hexadecimal notation. For example, the English double quotes are encoded as "%22".
        -   Extended UTF-8 characters are encoded in the "%XY%ZA…" format.
        -   Note that a space is encoded into "%20" instead of a plus sign "+".
        **Note:** Generally, libraries that support URL encoding \(for example, Java’s java.net.URLEncoder\) are all encoded according to the rules for the "application/x-www-form-urlencoded" MIME-type. If this encoding method is used, replace the plus signs "+" in the encoded strings with "%20", the asterisks "\*" with "%2A", and change "%7E" back to the tilde "~" to conform to the encoding rules described above.

    3.  Connect the encoded parameter names and values with the equal sign "=".
    4.  Then, sort the parameter name and value pairs connected by equal signs in alphabetical order, and connect them with the "&" symbol to produce the Canonicalized Query String.
2.  Follow the rules below to construct the string used for signature calculation by using the Canonicalized Query String constructed in the previous step:

    ```
    StringToSign=
     HTTPMethod + “&” +
     percentEncode(“/”) + ”&” +
     percentEncode(CanonicalizedQueryString)
    ```

    -   HTTPMethod is the HTTP method used for request submission, for example, GET.
    -   percentEncode\("/"\) is the coded value for the character "/" according to the URL encoding rules described in 1.ii, that is, "%2F".
    -   percentEncode\(CanonicalizedQueryString\) is the encoded string of the Canonicalized Query String constructed in Step 1, produced by following the URL encoding rules described in 1.ii.
3.  According to RFC2104 definitions, use the above signature sting to calculate the signature’s HMAC value.

    **Note:** The Key used for calculating the signature is the AccessKeySecret held by the user, which ends with the "&" character \(ASCII:38\) and is based on the SHA1 hashing.

4.  According to Base64 encoding rules, encode the above HMAC value into a string. This gives you the signature value.
5.  Add the obtained signature value to the request parameters as the Signature parameter. This completes the request signing process.

    **Note:** When the obtained signature value is submitted to the ECS server as the final request parameter value, the value is URL encoded like other parameters according to RFC3986 rules.

    Take DescribeScalingGroups as an example. The request URL prior to signing is as follows:

    ```
    http://ess.aliyuncs.com/?TimeStamp=2014-08-15T11%3A10%3A07Z&Format=xml&AccessKeyId=testid&Action=DescribeScalingGroups&SignatureMethod=HMAC-SHA1&RegionId=cn-qingdao&SignatureNonce=1324fd0e-e2bb-4bb1-917c-bd6e437f1710&SignatureVersion=1.0&Version=2014-08-28
    ```

    Thus, the StringToSign is:

    ```
    GET&%2F&AccessKeyId%3Dtestid&Action%3DDescribeScalingGroups&Format%3Dxml&RegionId%3Dcn-qingdao&SignatureMethod%3DHMAC-SHA1&SignatureNonce%3D1324fd0e-e2bb-4bb1-917c-bd6e437f1710&SignatureVersion%3D1.0&TimeStamp%3D2014-08-15T11%253A10%253A07Z&Version%3D2014-08-28
    ```

    Assume that the AccessKeyID is "testid", the AccessKeySecret is "testsecret", and the Key used for HMAC calculation is "testsecret&". The calculated signature value is "SmhZuLUnXmqxSEZ%2FGqyiwGqmf%2BM=".

    The signed request URL is \(added with the Signature parameter\):

    ```
    http://ess.aliyuncs.com/?TimeStamp=2014-08-15T11%3A10%3A07Z&Format=xml&AccessKeyId=testid&Action=DescribeScalingGroups&SignatureMethod=HMAC-SHA1&RegionId=cn-qingdao&SignatureNonce=1324fd0e-e2bb-4bb1-917c-bd6e437f1710&SignatureVersion=1.0&Version=2014-08-28&Signature=SmhZuLUnXmqxSEZ%2FGqyiwGqmf%2BM%3D
    ```


For more information about signatures and request submission, see [how to call interfaces](https://partners-intl.aliyun.com/help/faq-detail/25692.htm).

