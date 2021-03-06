## 1. 接口描述

注：本接口为改版后的 API 接口。如需了解旧接口相关信息，请参考：[解绑定弹性公网IP](/document/api/213/1376)。


本接口 (DisassociateAddress) 用于解绑[弹性公网IP](/document/product/213/1941)（简称 EIP）。

接口请求域名：<font style="color:red">eip.api.qcloud.com</font>

* 只有状态为 BIND 和 BIND_ENI 的 EIP 才能进行解绑定操作。
* EIP 如果被封堵，则不能进行解绑定操作。


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，其它参数见[公共请求参数](/document/api/213/6976)页面。

| 参数名称 | 类型 | 是否必选 | 描述 |
|---------|---------|---------|---------|
| Version |String|是|表示 API 版本号，主要用于标识请求的不同 API 版本。 本接口第一版本可传：2017-03-12。|
| AddressId | String| 是| 标识 EIP 的唯一 ID。EIP 唯一 ID 形如：`eip-11112222`。|
| ReallocateNormalPublicIp | String| 否| 表示解绑 EIP 之后是否分配普通公网 IP。取值范围：<br><li>TRUE：表示解绑 EIP 之后分配普通公网 IP。<br><li>FALSE：表示解绑 EIP 之后不分配普通公网 IP。<br>默认取值：FALSE。<br><br>只有满足以下条件时才能指定该参数：<br><li> 只有在解绑主网卡的主内网 IP 上的 EIP 时才能指定该参数。<br><li>解绑 EIP 后重新分配普通公网 IP 操作一个账号每天最多操作 10 次；详情可通过 [DescribeAddressQuota](/document/api/213/1378) 接口获取。 |


## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
|RequestId |String | 唯一请求 ID。每次请求都会返回`RequestId`。当用户调用接口失败找后台研发人员处理时需提供该`RequestId`。|


## 4. 错误码

以下错误码表仅列出了该接口的业务逻辑错误码，更多错误码详见[公共错误码](/document/api/213/10146)。

| 错误码 | 描述 |
|---------|---------|
|InvalidAddressId.NotFound|指定的 EIP 不存在。|
|InvalidAddressId.Blocked|指定 EIP 处于被封堵状态。当 EIP 处于封堵状态的时候是不能够进行解绑定操作的，需要先进行解封。|
|InvalidAddressIdStatus.NotPermit|指定 EIP 当前状态不能进行解绑定操作。只有 EIP 的状态处于 BIND 或 BIND_ENI 状态时才能进行解绑定操作。|
|InvalidInstanceId.NotFound|指定实例 ID 不存在。|
|InvalidInstance.NotSupported|指定实例当前状态不能进行解绑定 EIP 操作。|
|InvalidParameter|参数取值不合法。|
|AddressQuotaLimitExceeded.DailyAllocate| 重新分配普通公网 IP 配额已经到达当日配额上线。配额详情可通过 [DescribeAddressQuota](/document/api/213/1378) API 获取。|


## 5. 示例代码


### 示例1

> **解绑 EIP ：**<br>


#### 请求参数
<pre>
  https://cvm.api.qcloud.com/v2/index.php?Action=DisassociateAddress
  &Version=2017-03-12
  &AddressId=eip-ek0cdz1g
  &<<a href="/doc/api/229/6976">公共请求参数</a>>
</pre>

#### 返回参数
<pre>
{
    "Response": {
        "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
    }
}
</pre>


### 示例2

> **解绑 EIP 同时在解绑之后分配普通公网 IP：**<br>
> 只有在该 EIP 绑定在主网卡的主内网 IP 上时才支持。


#### 请求参数
<pre>
  https://cvm.api.qcloud.com/v2/index.php?Action=DisassociateAddress
  &Version=2017-03-12
  &AddressId=eip-ek0cdz1g
  &ReallocateNormalPublicIp=TRUE
  &<<a href="/doc/api/229/6976">公共请求参数</a>>
</pre>

#### 返回参数
<pre>
{
    "Response": {
        "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
    }
}
</pre>
