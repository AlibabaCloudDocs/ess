# Query a scaling rule {#concept_25950_zh .concept}

Queries information of a scaling rule.

## Description {#section_td2_zjk_sfb .section}

You can query all scaling rules in a scaling group by specifying the scaling group ID.

## Request parameters {#section_ilw_zjk_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface, required. The parameter value is DescribeScalingRules.|
|RegionId|String|Yes|Region ID of the scaling group of a scaling rule.|
|ScalingGroupId|String|No|Scaling group ID.|
|ScalingRuleId.N|String|No|ID of a scaling rule. A maximum of 10 values can be entered. Invalid scaling rule IDs are neglected in the query result and no error is reported.|
|ScalingRuleName.N|String|No|Name of a scaling rule. A maximum of 10 values can be entered. Invalid scaling rule names are neglected in the query result and no error is reported.|
|ScalingRuleAri.N|String|No|Unique identifier of a scaling rule. A maximum of 10 values can be entered. Invalid unique identifiers of scaling rules are neglected in the query result and no error is reported.|
|PageNumber|Integer|No|Page number of the scaling rule list. The initial value and default value are both 1.|
|PageSize|Integer|No|When querying by page, this parameter indicates the number of lines per page. Maximum value: 50; default value: 10.|

## Response parameters {#section_pbs_bkk_sfb .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of scaling rules|
|PageNumber|Integer|Current page number|
|PageSize|Integer|Number of lines per page|
|ScalingRules|ScalingRuleSetType|Scaling rule information set|

ScalingRuleSetType is a set of ScalingRuleItemTypes.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingRule|ScalingRuleItemType|Scaling rule information|

The attributes of ScalingRuleItemType are listed as follows.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingRuleId|String|ID of a scaling rule|
|ScalingGroupId|String|Scaling group ID|
|ScalingRuleName|String|Name of a scaling rule|
|Cooldown|Integer|Cool-down time|
|AdjustmentType|String|Adjustment mode|
|AdjustmentValue|Integer|Adjustment value|
|ScalingRuleAri|String|Unique identifier of a scaling rule|

## Error code {#section_ldw_hkk_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

## Request example {#section_as4_3kk_sfb .section}

```
http://ess.aliyuncs.com/?Action=DescribeScalingRules
&RegionId=cn-qingdao
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&PageSize=50
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<DescribeScalingRulesResponse>
    <PageNumber>1</PageNumber>
    <PageSize>50</PageSize>
    <ScalingRules>
        <ScalingRule>
            <AdjustmentType>QuantityChangeInCapacity</AdjustmentType>
            <AdjustmentValue>1</AdjustmentValue>
            <Cooldown>20</Cooldown>
            <ScalingGroupId>AG6CQdPU8OKdwLjgZcJ2eaQ</ScalingGroupId>          <ScalingRuleAri>
ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweNI1Ik
</ScalingRuleAri>
            <ScalingRuleId>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleId>            <ScalingRuleName>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleName>
        </ScalingRule>
    </ScalingRules>
    <TotalCount>1</TotalCount>
    <RequestId>3306A40D-3412-4101-9F19-5F81E3055DAD</RequestId>
</DescribeScalingRulesResponse>
```

JSON format:

```
{
  "RequestId": "B583BFEF-A779-427A-9B74-262DDD249702",
  "TotalCount": 1,
  "PageNumber": 1,
  "PageSize": 10,
  "ScalingRules": {
    "ScalingRule": [
      {
        "ScalingRuleId": "efcqrZdjlookc0UkE3dA5I0a",
        "ScalingRuleAri": "ari:acs:ess:cn-qingdao:1344371:scalingRule/efcqrZdjlookc0UkE3dA5I0a",
        "Cooldown": 500,
        "ScalingGroupId": "ccMvs9dcZlE5c9CtrwbXzizr",
        "AdjustmentType": "TotalCapacity",
        "ScalingRuleName": "KFJoxGKXXt",
        "AdjustmentValue": 5
      }
    ]
  }
}
```

