## 接口名称
ApplyUpload

## 功能说明
1. 整个视频上传分为申请上传、[上传文件](/document/product/266/9758)、[确认上传](/document/product/266/9757)三步，该接口为其中的第一步，如下图所示；
1. 申请视频上传，获取文件上传到腾讯云对象存储 COS 的元信息（包括上传路径、上传签名等）；
1. 如果需要额外上传一张本地图片作为封面，该接口亦可返回封面的上传信息；
1. 指定视频上传完成之后的处理方式。


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
| videoType | 是 | String | 视频文件类型 |
| videoName | 否 | String | 视频文件名称 |
| videoSize | 否 | Integer | 视频文件的大小(单位：字节) |
| coverType | 否 | String | 封面文件类型 |
| coverName | 否 | String | 封面文件名称 |
| coverSize | 否 | Integer | 封面文件的大小(单位：字节) |
| procedure | 否 | String | 视频后续任务操作，详见[任务流综述](/document/product/266/10263) |
| COMMON_PARAMS | 是 |  | 参见[公共参数](/document/product/266/7782#.E5.85.AC.E5.85.B1.E5.8F.82.E6.95.B0) |

### 请求示例

<pre>
https://vod.api.qcloud.com/v2/index.php?Action=ApplyUpload
&videoType=mp4
&coverType=jpg
&COMMON_PARAMS
</pre>

## 接口应答

### 参数说明
| 参数名称 | 类型 | 说明 |
|---------|---------|---------|
| code | Integer | 错误码。0：成功；其他值：失败 |
| message | String | 错误信息 |
| video | Object | 视频文件上传信息 |
| video.storagePath | String | 视频文件的上传路径 |
| cover | Object | 封面图片上传信息 |
| cover.storagePath | String | 封面图片的上传路径 |
| storageBucket | String | 视频和图片的存储bucket |
| storageRegion | String | 视频和图片的存储园区 |
| vodSessionKey | String | 整个上传流程的会话信息，在调用[结束上传](/document/product/266/9757)时会再次使用 |

### 错误码说明
| 错误码 | 含义说明|
|---------|---------|
| 4000-7000 | 参见[公共错误码](/document/product/266/7783) |
| 32001 | 服务内部错误  |

### 应答示例

```javascript
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "video": {
        "storagePath": "/6c0f1c00vodgzp251000333/dee2156d24820810452266402/f0.mp4"
    },
    "cover": {
        "storagePath": "/6c0f1c00vodgzp251000333/dee2156d24820810452266402/24820810452266403.jpg"
    },
    "storageBucket": "6c0f1c00vodgzp251000333",
    "storageRegion": "gzp",
    "vodSessionKey": "3KEGq9DWHl1xF819mM4jVFkGn5WON8"
}
```