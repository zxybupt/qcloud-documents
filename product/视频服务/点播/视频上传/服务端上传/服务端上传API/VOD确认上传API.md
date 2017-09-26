## 接口名称
CommitUpload

## 功能说明
1. 整个视频上传分为[申请上传](/document/product/266/9756)、[上传文件](/document/product/266/9758)、确认上传三步，该接口为其中的第三步，如下图所示；
1. 确认视频（以及封面）的上传，返回视频（以及封面）的播放地址URL、视频FileID；
1. 如果在申请上传时指定了视频处理过程，则点播后台将发起对视频处理操作，并返回任务ID。

**注意：**
> 视频上传整体逻辑较为复杂，建议使用点播封装的**服务端上传SDK**来进行上传，而非直接调用该接口。参见：[服务端上传综述](/document/product/266/9759)。

## 请求方式

### 请求域名
vod.api.qcloud.com

### 最高调用频率
100次/分钟

### 参数说明
| 参数名称 | 必填 | 类型 | 说明 |
|---------|---------|---------|---------|
| vodSessionKey | 是 | String | 调用[申请上传](/document/product/266/9756)时获取的会话信息 |
| COMMON_PARAMS | 是 |  | 参见[公共参数](/document/product/266/7782#.E5.85.AC.E5.85.B1.E5.8F.82.E6.95.B0) |

### 请求示例

<pre>
https://vod.api.qcloud.com/v2/index.php?Action=CommitUpload
&vodSessionKey=3KEGq9DWHl1xF819mM4jVFkGn5WON8
&COMMON_PARAMS
</pre>

## 接口应答

### 参数说明

| 参数名称 | 类型 | 说明 |
|---------|---------|---------|
| code | Integer | 错误码。0：成功；其他值：失败 |
| message | String | 错误信息 |
| video | Object | 视频源文件上传结果 |
| video.url | String | 视频源文件播放地址 |
| cover | Object | 封面图片上传结果 |
| cover.url | Object | 封面图片地址 |
| fileId | String | 视频文件的文件ID |


### 错误码说明
| 错误码 | 含义说明|
|---------|---------|
| 4000-7000 | 参见[公共错误码](/document/product/266/7783)  |
| 31001 | vodSessionKey非法  |
| 32001 | 服务内部错误 |

### 应答示例
```javascript
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "video": {
        "url": "http://251000333.vod2.myqcloud.com/6c0f1c00vodgzp251000333/dee2125c24820810452266399/f0.mp4"
    },
    "cover": {
        "url": "http://251000333.vod2.myqcloud.com/6c0f1c00vodgzp251000333/dee2125c24820810452266399/24820810452266400.jpg"
    },
    "fileId": "24820810452266399"
}
```