# 智能音频文件识别产品API文档

- - - - -

***版权所有 翻版必究***

- - - - -

目录

- [智能音频文件识别产品API文档](#智能音频文件识别产品api文档)
- [1. 接入前准备](#1-接入前准备)
  - [1.1 数美服务账号申请](#11-数美服务账号申请)
  - [1.2 渠道配置表](#12-渠道配置表)
  - [1.3 数美服务账号信息接收](#13-数美服务账号信息接收)
- [2. 智能音频识别服务接口说明](#2-智能音频识别服务接口说明)
  - [2.1 上传音频识别请求](#21-上传音频识别请求)
    - [接口描述](#接口描述)
    - [请求URL](#请求url)
    - [字符编码格式](#字符编码格式)
    - [请求方法](#请求方法)
    - [建议超时时长](#建议超时时长)
    - [音频格式限制](#音频格式限制)
    - [请求体限制](#请求体限制)
    - [请求参数](#请求参数)
    - [返回参数](#返回参数)
    - [示例](#示例)
      - [上传url音频数据请求示例](#上传url音频数据请求示例)
      - [上传base64音频数据请求示例](#上传base64音频数据请求示例)
      - [返回示例](#返回示例)
  - [2.2 主动查询识别结果](#22-主动查询识别结果)
    - [接口描述](#接口描述-1)
    - [请求URL](#请求url-1)
    - [字符编码格式](#字符编码格式-1)
    - [请求方法](#请求方法-1)
    - [建议超时时长](#建议超时时长-1)
    - [请求参数](#请求参数-1)
    - [返回参数](#返回参数-1)
    - [示例](#示例-1)
      - [请求示例](#请求示例)
      - [返回示例](#返回示例-1)
  - [2.3 异步回调识别结果](#23-异步回调识别结果)
    - [支持协议](#支持协议)
    - [字符编码格式](#字符编码格式-2)
    - [请求方法](#请求方法-2)
    - [建议超时时长](#建议超时时长-2)
    - [推送策略](#推送策略)
    - [返回字段](#返回字段)
- [3. FAQ](#3-faq)
  - [3.1 调用接口返回参数错误（1902）](#31-调用接口返回参数错误1902)
  - [3.2 调用接口返回无权限操作（9101）](#32-调用接口返回无权限操作9101)
  - [3.3 调用接口超时问题](#33-调用接口超时问题)

# 1. 接入前准备

## 1.1 数美服务账号申请

客户经理已提前与贵公司建立联系或当面拜访，可直接将开通账号及服务相关信息提供至客户经理。

开通账号所需信息包括：

公司全称：xxxxxx

公司简称：xxxxxx

接口人邮箱：xxx@xxx.xxx

接口人手机：1xxxxxxxxxx

## 1.2 渠道配置表

数美根据客户不同业务场景，配置不同的渠道（channel），制定针对性的拦截策略，同时也方便客户针对不同业务场景的数据进行筛选、分析。业务场景和渠道取值对应表如下（支持客户自定义）：

| **业务场景** | **channel取值** | **备注** |
| :----------: | :-------------: | :------: |
|   语音文件   |      AUDIO      |          |

## 1.3 数美服务账号信息接收

数美客户经理会在1个工作日内为您开通相应数美账号及服务，随后接口人邮箱会收到如下信息：

| **名称**         | **具体值**                    | **说明**                                    |
| :--------------- | :---------------------------- | :------------------------------------------ |
| accessKey        | xxxxxx                        | 数美API服务的认证码，调用数美API时需要传入  |
| organization     | xxxxxx                        | 数美分配的企业唯一标识码，调用SDK时需要传入 |
| 数美管理后台账号 | xxxxxx                        | 用于登陆数美管理后台                        |
| 数美管理后台密码 | xxxxxx                        | 用于登陆数美管理后台                        |
| 数美管理后台地址 | https://www.fengkongcloud.com | 用于登陆数美管理后台                        |

# 2. 智能音频识别服务接口说明

## 2.1 上传音频识别请求

### 接口描述

该接口用于提交音频识别请求。

### 请求URL

上海集群：

http://api-audio-sh.fengkongcloud.com/v2/saas/anti_fraud/audio

硅谷集群：

http://api-audio-gg.fengkongcloud.com/v2/saas/anti_fraud/audio

### 字符编码格式

使用UTF-8字符集进行编码

### 请求方法

POST

### 建议超时时长

3s

### 音频格式限制

`WAV`、`MP3`、`AAC`、`AMR`、`3GP`、`M4A`、`WMA`、`OGG`、`APE`、`FLAC`、`ALAC`、`WAVPACK`、`SILK_V3`等

### 请求体限制

所有请求参数大小总和不能超过18M

### 请求参数

放在HTTP Body中，采用Json格式，具体参数如下：

| **参数名称**  | **类型**    | **是否必选** | **说明**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| :------------ | :---------- | :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| accessKey     | string      | Y            | 服务密匙，开通账号服务时由数美提供                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| type          | string      | Y            | <p>需要识别的违规类型，可选值：</p><p>AUDIOPOLITICAL：一号领导人声纹识别</p><p>POLITICS：涉政识别</p><p>ANTHEN：国歌识别</p><p>PORN：色情</p><p>ABUSE: 辱骂识别</p><p>AD：广告识别</p><p>MOAN：娇喘识别</p><p>GENDER：性别识别</p><p>TIMBRE：音色标签（需要同时传入GENDER才能生效）</p><p>SING：唱歌识别</p><p>LANGUAGE：语种识别</p><p>MINOR：未成年识别</p><p>BANEDAUDIO：违禁歌曲</p><p>VOICE：人声属性</p><p>AUDIOSCENE：声音场景</p><p>如需做组合识别，通过下划线连接即可，例</p><p>如 POLITICS_PORN_AD用于广告、色情和涉政识别。<br/>建议传入：<br/>POLITICS_PORN_AD_MOAN</p> |
| functionType  | string      | N            | <p>可选值：</p><p>`COPYRIGHT`：版权识别</p><p>如需做组合识别，通过下划线连接即可</p>                                                                                                                                                                                                                                                                                                                                                                              |
| appId         | string      | N            | 应用标识，此字段强校验，需要提前与数美约定好取值。不传取默认值default                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| btId          | string      | Y            | 音频唯一标识，限长128位字符长度, 不能重复，否则提示参数错误。                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| data          | json_object | Y            | 请求数据，最长1MB，详细内容参见下表                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| callback      | string      | N            | 异步检测结果回调通知您的URL，支持HTTP和HTTPS。字段为空时，您必须通过查询接口主动查询结果。                                                                                                                                                                                                                                                                                                                                                                                                              |
| callbackParam | json_object | N            | 透传字段，当 callback 存在时可选，发送回调请求时服务将该字段内容同音频结果一起返回                                                                                                                                                                                                                                                                                                                                                                                                                      |

*data的内容如下：*

| **参数名称**  | **类型**    | **是否必选** | **说明**                                                                                                                                                                    |
| :------------ | :---------- | :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| url           | string      | N            | 待识别音频url地址，url和content至少提供一个                                                                                                                                 |
| lang          | string      | N            | 可选值如下，（默认值为zh）：<br/>zh：中文<br/>en：英文<br/>ar：阿拉伯语                                                                                                     |
| content       | string      | N            | 待识别音频的base64编码数据（上限15M，仅支持pcm、wav、mp3）, pcm格式数据必须采用16-bit小端序编码。推荐使用pcm、wav格式传输。url和content至少提供一个，同时存在时仅支持content |
| formatInfo    | json_object | N            | 当content存在时必须存在，本地语音文件格式信息。json内具体格式见下方说明                                                                                                     |
| audioName     | string      | N            | 音频文件名称                                                                                                                                                                |
| tokenId       | string      | N            | 用户账号标识                                                                                                                                                                |
| channel       | string      | N            | 业务场景名称，见渠道配置表                                                                                                                                                  |
| returnAllText | bool        | N            | 取值为true时，返回所有音频片段识别结果（每10秒一个音频片段）；取值为false时，返回风险片段（riskLevel为REJECT或REVIEW）识别结果。默认为false。                               |
| nickname      | string      | N            | 用户昵称                                                                                                                                                                    |
| timestamp     | int         | N            | 时间戳（毫秒级）                                                                                                                                                            |
| room          | string      | N            | 房间号                                                                                                                                                                      |
| copyright     | json_object | N            | 该字段在functionType字段含有COPYRIGHT类型时生效                                                                                                                |

*formatInfo内容如下：*

| **参数名称** | **类型** | **是否必选** | **说明**                                                                          |
| :----------- | :------- | :----------- | :-------------------------------------------------------------------------------- |
| format       | string   | Y            | 语音数据格式，仅支持（取值）pcm、wav、mp3，严格小写。                             |
| rate         | int      | N            | 语音数据采样率，当语音数据格式为pcm时必须存在，范围限制8000-32000。               |
| track        | int      | N            | 语音数据声道数，当语音数据格式为pcm时必须存在，支持单声道(取值1)或双声道(取值2)。 |

*copyright的内容如下：*

| **参数名称** | **类型**   | **是否必选**   | **说明**                                                                          |
| :----------- | :------- | :----------- | :-------------------------------------------------------------------------------- |
| resultCount  | int      | N            | 非必传，默认返回top 1<br/>取值范围（0，20]，仅支持正整数格式<br/>将匹配结果按照相似度排序，只返回重复文章的前top K的结果 |
| categoryId   | string   | N            | 客户在管理样本库时可以创建多个样本库，通过该字段控制本次请求数据与哪一个样本库做匹配<br/>非必传，若客户不传，则默认为ALL，与全部样本库做匹配<br/>ALLOWLIST表示白样本库<br/>BLOCKLIST表示黑样本库<br/>可以传多个，用下划线_连接，例如ALLOWLIST_BLOCKLIST |


### 返回参数

放在HTTP Body中，采用Json格式，具体参数如下：

| **参数名称** | **类型** | **是否必选** | **说明**                                         |
| :----------- | :------- | :----------- | :----------------------------------------------- |
| code         | int      | Y            | 返回码                                           |
| message      | string   | Y            | 返回码详情描述                                   |
| requestId    | string   | Y            | 请求唯一标识                                     |
| btId         | string   | Y            | 客户上传音频唯一标识，与请求参数中的btId字段对应 |

code和message的列表如下：

| **code** | **message** |
| :------- | :---------- |
| 1100     | 成功        |
| 1901     | QPS超限     |
| 1902     | 参数不合法  |
| 1903     | 服务失败    |
| 9100     | 余额不足    |
| 9101     | 无权限操作  |

### 示例

#### 上传url音频数据请求示例

```json
{
    "accessKey":"****************",
    "type": "DEFAULT",
    "functionType": "COPYRIGHT",
    "appId": "default",
    "btId": "test01",
    "data": {
        "tokenId": "test_01",
        "url": "http://xxxxxxxx.mp3",
        "channel": "IM_MESSAGE",
        "returnAllText": true,
        "copyright": {
          "resultCount": 10,
          "categoryId": "ALLOWLIST_BLOCKLIST"
        }
    },
    "callback": "http://xxxxxxxxx",
    "callbackParam": {
        " param1": 1,
        " param2": "qew",
        " param3": true
    }
}
```

#### 上传base64音频数据请求示例

```json
{
    "accessKey": "****************",
    "type": "DEFAULT",
    "functionType": "COPYRIGHT",
    "appId": "default",
    "btId": "test01",
    "data": {
        "content": "音频base64编码数据",
        "formatInfo": {
            "format": "pcm",
            "rate": 16000,
            "track": 1
        },
        "channel": "IM_MESSAGE",
        "tokenId": "asdwef",
        "returnAllText": true,
        "copyright": {
          "resultCount": 10,
          "categoryId": "ALLOWLIST_BLOCKLIST"
        }
    },
    "callback": "http://xxxxxx",
    "callbackParam": {
        "param1": 1,
        "param2": "qew",
        "param3": true
    }
}
```

#### 返回示例

```json
{
    "code":1100,
    "message":"成功",
    "requestId":" XXXXXXXXXXXX",
    "btId":"XXXXXXX"
}
```

## 2.2 主动查询识别结果

### 接口描述

该接口用于查询音频识别结果，最大支持10qps。

### 请求URL

上海集群：

http://api-audio-sh.fengkongcloud.com/v2/saas/anti_fraud/query_audio

### 字符编码格式

请求及返回结果都使用UTF-8字符集进行编码

### 请求方法

POST

### 建议超时时长

1s

### 请求参数

放在HTTP Body中，采用Json格式，具体参数如下：

| **参数名称** | **类型** | **是否必选** | **说明**                           |
| :----------- | :------- | :----------- | :--------------------------------- |
| accessKey    | string   | Y            | 服务密匙，开通账号服务时由数美提供 |
| btId         | string   | Y            | 音频唯一标识，用于查询识别结果     |

### 返回参数

放在HTTP Body中，采用Json格式，具体参数如下：

| **参数名称**   | **类型**    | **是否必选** | **说明**                                                     |
| :------------- | :---------- | :----------- | :----------------------------------------------------------- |
| code           | int         | Y            | 返回码                                                       |
| message        | string      | Y            | 返回码详情描述                                               |
| requestId      | string      | Y            | 请求唯一标识                                                 |
| btId           | string      | Y            | 音频唯一标识                                                 |
| audioText      | string      | Y            | 整段音频转译文本结果                                         |
| audioTime      | int         | N            | 整段音频的音频时长，单位秒，code为1100时存在                 |
| labels         | string      | N            | 音频识别结果标签                                             |
| riskLevel      | string      | N            | <p>识别结果，可能返回值：</p><p>PASS：正常内容<br/>REVIEW：疑似违规内容<br/>REJECT：违规内容</p> |
| detail         | json_array  | N            | 风险详情                                                     |
| gender         | json_object | N            | 性别标签与概率值                                             |
| isSing         | int         | N            | <p>表示该条音频文件是否唱歌，0表示没有唱歌，1表示唱歌。</p><p>仅当type传入值包含SING时返回。</p> |
| language       | json_array  | N            | 语种标签与概率值列表                                         |
| tags           | json_array  | N            | 音色标签与概率值列表                                         |
| businessLabels | json_array  | N            | 业务标签返回（目前只支持MINOR,策略命中返回标签内容,否则为空） |
| copyright      | json_array  | N            | 版权重复结果详情，当functionType取值包含`COPYRIGHT`时返回，有可能为空数组 |

*detail数组中每一项的具体参数如下：*

| **参数名称**     | **类型** | **是否必选** | **说明**                                                                                                                                                                                                                                                                                                       |
| :--------------- | :------- | :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| requestId        | string   | Y            | 风险音频片段请求唯一标识                                                                                                                                                                                                                                                                                       |
| audioStarttime   | string   | Y            | 风险音频片段在音频中的起始时间，单位秒                                                                                                                                                                                                                                                                         |
| audioEndtime     | string   | Y            | 风险音频片段在音频中的结束时间，单位秒                                                                                                                                                                                                                                                                         |
| audioUrl         | string   | Y            | 风险音频片段地址，MP3格式                                                                                                                                                                                                                                                                                      |
| audioText        | string   | Y            | 音频片段转译的文本内容                                                                                                                                                                                                                                                                                         |
| riskLevel        | string   | Y            | <p>识别结果，可能返回值： <br/>REJECT：违规内容</p><p>REVIEW：疑似违规内容</p><p>PASS：正常内容</p>                                                                                                                                                                                                            |
| riskType         | int      | N            | <p>标识风险类型，可能取值:<br/>风险类型，静音时不返回，可能取值:<br/>0:正常</p><p>100:涉政</p><p>110:暴恐</p><p>120:国歌</p><p>200:色情</p><p>210:辱骂</p><p>250:娇喘</p><p>260:一号领导声纹</p><p>270:人声属性</p><p>280:违禁歌曲</p><p>300:广告</p><p>400:灌水</p><p>500:无意义</p><p>600:违禁</p><p>700:其他</p><p>720:黑账号</p><p>730:黑IP</p><p>800:高危账号</p><p>900:自定义</p> |
| audioMatchedItem | string   | N            | 音频中可能出现的敏感词                                                                                                                                                                                                                                                                                         |
| description      | string   | Y            | 音频片段风险原因描述                                                                                                                                                                                                                                                                                           |

*gender参数结构如下：*

| **参数名称** | **类型** | **是否必选** | **说明**                                              |
| :----------- | :------- | :----------- | :---------------------------------------------------- |
| label        | string   | Y            | <p>性别标签名称，可能取值：</p><p>男性</p><p>女性</p> |
| confidence   | int      | Y            | 对应性别可能性大小，取值0-100，数值越高表示概率越大。 |

*language数组中每一项具体参数如下：*

| **参数名称** | **类型** | **是否必选** | **说明**                                                                     |
| :----------- | :------- | :----------- | :--------------------------------------------------------------------------- |
| label        | int      | Y            | <p>语种识别类别标识，可能取值：</p><p>0:普通话</p><p>1:英语</p><p>2:粤语</p> |
| confidence   | int      | Y            | 对应语种标签可能性大小，取值0-100，数值越高表示概率越大。                    |

*tags数组中每一项具体参数如下：*

| **参数名称** | **类型** | **是否必选** | **说明**                                                                                                                                                              |
| :----------- | :------- | :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label        | string   | Y            | <p>音色标签类别，可能取值：</p><p>大叔</p><p>青年</p><p>正太</p><p>老年</p><p>女王</p><p>御姐</p><p>少女</p><p>萝莉</p><p>大妈</p><p>男性</p><p>女性</p><p>无人声</p> |
| confidence   | int      | Y            | 对应音色标签可能性大小，取值0-100，数值越高表示概率越大。                                                                                                             |

*businessLabels数组中每一项具体参数如下：*

| **参数名称**        | **类型** | **是否必返** | **说明**                         |
| :------------------ | :------- | :----------- | :------------------------------- |
| businessLabel1      | string   | Y            | 注意：businessLabels不为空时必返 |
| businessLabel2      | string   | Y            | 注意：businessLabels不为空时必返 |
| businessLabel3      | string   | Y            | 注意：businessLabels不为空时必返 |
| businessDescription | string   | Y            | 注意：businessLabels不为空时必返 |

*copyright数组中每一项具体参数如下：*

| **参数名称**  | **类型** | **是否必返** | **说明**                                 |
| :------------| :-----  | :----------| :--------------------------------------- |
| chapter      | string  | Y          |匹配的章节标题                               |
| similarity   | float   | Y          |本次检测的数据与命中的样本的相似度，取值范围(0，1] |
| categoryId   | string  | Y          |表示该命中结果所属的样本库ID                   |

code和message的列表如下：

| **code** | **message** |
| :------- | :---------- |
| 1100     | 成功        |
| 1101     | 正在处理中  |
| 1902     | 参数不合法  |
| 1903     | 服务失败    |
| 9100     | 余额不足    |
| 9101     | 无权限操作  |

### 示例

#### 请求示例

```json
{
    "accessKey":"*************",
    "btId":"xxxx"
}
```

#### 返回示例

```json
{
    "code": 1100,
    "message": "成功",
    "requestId": "b891cf2d82e214de45df33fc2bea4875",
    "btId": "xxxx",
    "riskLevel": "REJECT",
    "audioText": "法轮大法好",
    "labels": "涉政-音频",
    "detail": [
        {
            "audioStarttime": 10,
            "audioEndtime": 20,
            "audioUrl": "<http://xxxxxxxx.>wav ",
            "audioText": "法轮大法好",
            "riskLevel": "REJECT",
            "audioMatchedItem": "法轮",
            "riskType": 100,
            "description": "涉政-音频"
        }
    ],
    "tags": [
        {
            "label": "男性",
            "confidence": 90
        },
        {
            "label": "大叔音",
            "confidence": 91
        },
        {
            "label": "正太音",
            "confidence": 21
        },
        {
            "label": "老年音",
            "confidence": 11
        },
        {
            "label": "青年音",
            "confidence": 31
        }
      ],
    "copyright":[
      {
        "categoryId": "ALLOWLIST",
        "chapter":"测试1_章节1",
        "similarity":0.33
      },
      {
        "categoryId": "ALLOWLIST",
        "chapter":"测试1_章节2",
        "similarity":0.33
      },
      {
        "categoryId": "BLOCKLIST",
        "chapter":"测试2_章节1",
        "similarity":0.33
      }
    ]
}
```

## 2.3 异步回调识别结果

用户如果需要服务端主动对音频检测结果进行回调，则需要在请求参数中传入callback参数，服务端审核完成后将识别结果主动回调到该地址。

### 支持协议

HTTP 或 HTTPS

### 字符编码格式

请求使用 UTF-8 字符集进行编码

### 请求方法

POST

### 建议超时时长

5s

### 推送策略

当用户收到推送结果，并返回 HTTP 状态码为200时，表示推送成功；否则系统将进行最多10次推送。

### 返回字段

放在HTTP Body中，采用Json格式，具体参数如下：

| **参数名称**  | **类型**    | **是否必选** | **说明**                                                                                         |
| :------------ | :---------- | :----------- | :----------------------------------------------------------------------------------------------- |
| code          | int         | Y            | 返回码                                                                                           |
| message       | string      | Y            | 返回码详情描述                                                                                   |
| requestId     | string      | Y            | 请求唯一标识                                                                                     |
| btId          | string      | Y            | 音频唯一标识                                                                                     |
| audioText     | string      | Y            | 音频转译文本结果                                                                                 |
| audioTime     | int         | N            | 整段音频的音频时长，单位秒，code为1100时存在                                                     |
| labels        | string      | N            | 音频片段风险原因汇总                                                                             |
| riskLevel     | string      | N            | <p>识别结果，可能返回值：</p><p>PASS：正常内容<br/>REVIEW：疑似违规内容<br/>REJECT：违规内容</p> |
| detail        | json_array  | N            | 风险详情                                                                                         |
| gender        | json_object | N            | 性别标签与概率值                                                                                 |
| tags          | json_array  | N            | 音色标签与概率值列表                                                                             |
| copyright     | json_array  | N            | 版权重复结果详情，当functionType取值包含`COPYRIGHT`时返回，有可能为空数组 |
| callbackParam | json_object | Y            | 客户传入的透传字段                                                                               |

*detail数组中每一项的具体参数如下：*

| **参数名称**     | **类型** | **是否必选** | **说明**                                                                                                                                                                                                                                                                |
| :--------------- | :------- | :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| audioStarttime   | int      | Y            | 风险音频片段在音频中的起始时间，单位秒                                                                                                                                                                                                                                  |
| audioEndtime     | int      | Y            | 风险音频片段在音频中的结束时间，单位秒                                                                                                                                                                                                                                  |
| audioUrl         | string   | Y            | 风险音频片段地址                                                                                                                                                                                                                                                        |
| audioText        | string   | Y            | 音频片段对应的文本内容                                                                                                                                                                                                                                                  |
| riskLevel        | string   | Y            | <p>识别结果，可能返回值： <br/>REJECT：违规内容</p><p>REVIEW：疑似违规内容</p>                                                                                                                                                                                          |
| riskType         | int      | N            | <p>标识风险类型，可能取值:<br/>风险类型，静音时不返回，可能取值:<br/>0:正常</p><p>100:涉政</p><p>110:暴恐</p><p>120:国歌</p><p>200:色情</p><p>210:辱骂</p><p>250:娇喘</p><p>260:一号领导声纹</p><p>270:人声属性</p><p>280:违禁歌曲</p><p>300:广告</p><p>400:灌水</p><p>500:无意义</p><p>600:违禁</p><p>700:其他</p><p>720:黑账号</p><p>730:黑IP</p><p>800:高危账号</p><p>900:自定义</p> |
| audioMatchedItem | string   | N            | 音频中可能出现的敏感词                                                                                                                                                                                                                                                  |
| description      | string   | Y            | 风险原因描述                                                                                                                                                                                                                                                            |

*gender参数结构如下：*

| **参数名称** | **类型** | **是否必选** | **说明**                                              |
| :----------- | :------- | :----------- | :---------------------------------------------------- |
| label        | string   | Y            | <p>性别标签名称，可能取值：</p><p>男性</p><p>女性</p> |
| confidence   | int      | Y            | 对应性别可能性大小，取值0-100，数值越高表示概率越大。 |

*language数组中每一项具体参数如下：*

| **参数名称** | **类型** | **是否必选** | **说明**                                                                                                                                             |
| :----------- | :------- | :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| label        | int      | Y            | <p>语种识别类别标识，可能取值：</p><p>-1:其他语种</p><p>0:普通话</p><p>1:英语</p><p>2:粤语</p><p>3:藏语</p><p>4:维语</p><p>5:蒙语</p><p>6:朝鲜语</p> |
| confidence   | int      | Y            | 对应语种标签可能性大小，取值0-100，数值越高表示概率越大。                                                                                            |

*tags数组中每一项具体参数如下：*

| **参数名称** | **类型** | **是否必选** | **说明**                                                                                                                                             |
| :----------- | :------- | :----------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| label        | string   | Y            | <p>音色标签类别，可能取值：</p><p>大叔音</p><p>青年音</p><p>正太音</p><p>老年音</p><p>女王音</p><p>御姐音</p><p>少女音</p><p>萝莉音</p><p>大妈音</p> |
| confidence   | int      | Y            | 对应音色标签可能性大小，取值0-100，数值越高表示概率越大。                                                                                            |

*copyright数组中每一项具体参数如下：*

| **参数名称**  | **类型** | **是否必返** | **说明**                                 |
| :------------| :-----  | :----------| :--------------------------------------- |
| chapter      | string  | Y          |匹配的章节标题                               |
| similarity   | float   | Y          |本次检测的数据与命中的样本的相似度，取值范围(0，1] |
| categoryId   | string  | Y          |表示该命中结果所属的样本库ID                   |

# 3. FAQ

## 3.1 调用接口返回参数错误（1902）

答：调用数美接口时，code返回1902参数不合法，一般为客户输入的参数格式存在问题，客户可自行分析一下请求格式是否按照接口文档输入，或将请求的数据及返回数据反馈给数美分析解决。

## 3.2 调用接口返回无权限操作（9101）

答：调用数美接口时，code返回9101无权限操作，一般为调用了未开通的服务，沟通确认客户调用的服务接口，开通相应的服务。

## 3.3 调用接口超时问题

答：有如下两个常见问题：

1）DNS问题:

客户通过公网调用数美接口进行测试，客户DNS解析域名较慢，导致第一次请求超时，建议客户更换DNS，不建议客户在host中将域名和ip做绑定，数美更换接口IP导致无法请求接口。

2）网络问题:

客户通过公网调用数美接口，公网网络延迟较长，导致少量请求存在超时。可以建议客户ping数美不同的集群网络，建议客户接入网络延迟较低的数美集群。
