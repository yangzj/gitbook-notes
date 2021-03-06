# ContentRpcService.proto 接口文档

*Document generated by protoc-gen-markdown. DO NOT EDIT.*

> 接口列表


* 信息管理服务

	* 创建内容 - (/v1/cmc/content)
	* 查根据ID查询内容详情 - (/v1/cmc/content/{id}/{types})
	* 修改内容信息 - 部分更新 - (/v1/cmc/content)
	* 删除内容 - 批量 - (/v1/cmc/content/{id})

<h2 id="contentrpcservice"> 信息管理服务</h2>


<h3 id="createcontent"> 创建内容</h3>


* HTTP Gateway
	* URL: `/v1/cmc/content`
	* Method: `POST`
	* Content-Type: `application/json`

* 请求类型: ***ContentInfo***

>  内容详情

| 字段             | protobuf 类型                                        | json 类型      | 说明                          |
| ---------------- | ---------------------------------------------------- | -------------- | ----------------------------- |
| repositoryId     | int64                                                | string         | 空间ID                        |
| id               | int64                                                | string         | id                            |
| title            | string                                               | string         | 标题                          |
| description      | string                                               | string         | 描述                          |
| fromId           | int64                                                | string         | 来源                          |
| fromType         | enum [ContentFromType](#contentfromtype)             | string/integer | 来源分类                      |
| themeColor       | string                                               | string         | 主题颜色                      |
| topColor         | string                                               | string         | 颜色TOP5                      |
| priClassify      | int                                                  | number/string  | 一级分类（编辑器类型）        |
| secClassify      | string                                               | string         | 二级分类 (编辑器类型)         |
| version          | int                                                  | number/string  | 版本号                        |
| createdAt        | int64                                                | string         | 创建时间                      |
| updatedAt        | int64                                                | string         | 更新时间                      |
| type             | enum [RepositoryContentType](#repositorycontenttype) | string/integer | 类型                          |
| preview          | [PreViewInfo](#previewinfo)                          | object         | 预览图                        |
| compositePreview | [PreViewInfo](#previewinfo)                          | object         | 合成预览图                    |
| extendsPreview   | array [[PreViewInfo](#previewinfo)]                  | array          | 扩展预览图                    |
| design           | [DesignInfo](#designinfo)                            | object         | 设计文件详情                  |
| origin           | [OriginInfo](#origininfo)                            | object         | 源文件                        |
| playUrl          | string                                               | string         | 播放地址                      |
| categoryIds      | array [int64]                                        | string         | 分类ID列表                    |
| shot             | int                                                  | number/string  | 是否更新截图(0:不更新,1:更新) |
| tagIds           | array [int64]                                        | string         | 标签ID列表                    |
| sort             | int                                                  | number/string  | 内容排序值                    |


> JSON 示例

```json
{
  "repositoryId": "string($int64)",
  "id": "string($int64)",
  "title": "string",
  "description": "string",
  "fromId": "string($int64)",
  "fromType": "WEB | LOCAL | VEGETABLE_MARKET | VCG | GD | QIPING",
  "themeColor": "string",
  "topColor": "string",
  "priClassify": 0,
  "secClassify": "string",
  "version": 0,
  "createdAt": "string($int64)",
  "updatedAt": "string($int64)",
  "type": "TEMPLATE | IMAGE | VIDEO | MUSIC | FONT",
  "preview": {
    "id": "string($int64)",
    "imageUrl": "string",
    "partVideoUrl": "string",
    "videoUrl": "string",
    "width": 0,
    "height": 0,
    "hex": "string",
    "type": "PREVIEW_IMG | COMPOSITE_IMG | EXTEND_IMG | PREVIEW_GIF"
  },
  "compositePreview": {
    "id": "string($int64)",
    "imageUrl": "string",
    "partVideoUrl": "string",
    "videoUrl": "string",
    "width": 0,
    "height": 0,
    "hex": "string",
    "type": "PREVIEW_IMG | COMPOSITE_IMG | EXTEND_IMG | PREVIEW_GIF"
  },
  "extendsPreview": [
    {
      "id": "string($int64)",
      "imageUrl": "string",
      "partVideoUrl": "string",
      "videoUrl": "string",
      "width": 0,
      "height": 0,
      "hex": "string",
      "type": "PREVIEW_IMG | COMPOSITE_IMG | EXTEND_IMG | PREVIEW_GIF"
    }
  ],
  "design": {
    "id": "string($int64)",
    "url": "string",
    "size": "string($int64)",
    "containMaterial": [
      "string"
    ],
    "dpi": "string($int64)",
    "orientation": "HORIZONTAL | VERTICAL",
    "ext": "string"
  },
  "origin": {
    "id": "string($int64)",
    "url": "string",
    "size": "string($int64)",
    "dpi": 0
  },
  "playUrl": "string",
  "categoryIds": [
    "string($int64)"
  ],
  "shot": 0,
  "tagIds": [
    "string($int64)"
  ],
  "sort": 0
}
```



* 返回类型: ***Int64Value***

>  Wrapper message for `int64`.
>
>  The JSON representation for `Int64Value` is JSON string.

| 字段  | protobuf 类型 | json 类型 | 说明             |
| ----- | ------------- | --------- | ---------------- |
| value | int64         | string    | The int64 value. |

> JSON 示例

```json
{
  "value": "string($int64)"
}
```



<h3 id="querycontentbyid"> 查根据ID查询内容详情</h3>


* HTTP Gateway
	* URL: `/v1/cmc/content/{id}/{types}`
	* Method: `GET`
	* Content-Type: `application/json`

* 请求类型: ***QueryContentByIdRequest***

>  根据ID查询内容详情

| 字段  | protobuf 类型 | json 类型      | 说明     |
| ----- | ------------- | -------------- | -------- |
| id    | int64         | string         | 资源ID   |
| types | array [types] | string/integer | 过滤类型 |


* 返回类型: ***ContentInfo***

>  内容详情

| 字段             | protobuf 类型                                        | json 类型      | 说明                          |
| ---------------- | ---------------------------------------------------- | -------------- | ----------------------------- |
| repositoryId     | int64                                                | string         | 空间ID                        |
| id               | int64                                                | string         | id                            |
| title            | string                                               | string         | 标题                          |
| description      | string                                               | string         | 描述                          |
| fromId           | int64                                                | string         | 来源                          |
| fromType         | enum [ContentFromType](#contentfromtype)             | string/integer | 来源分类                      |
| themeColor       | string                                               | string         | 主题颜色                      |
| topColor         | string                                               | string         | 颜色TOP5                      |
| priClassify      | int                                                  | number/string  | 一级分类（编辑器类型）        |
| secClassify      | string                                               | string         | 二级分类 (编辑器类型)         |
| version          | int                                                  | number/string  | 版本号                        |
| createdAt        | int64                                                | string         | 创建时间                      |
| updatedAt        | int64                                                | string         | 更新时间                      |
| type             | enum [RepositoryContentType](#repositorycontenttype) | string/integer | 类型                          |
| preview          | [PreViewInfo](#previewinfo)                          | object         | 预览图                        |
| compositePreview | [PreViewInfo](#previewinfo)                          | object         | 合成预览图                    |
| extendsPreview   | array [[PreViewInfo](#previewinfo)]                  | array          | 扩展预览图                    |
| design           | [DesignInfo](#designinfo)                            | object         | 设计文件详情                  |
| origin           | [OriginInfo](#origininfo)                            | object         | 源文件                        |
| playUrl          | string                                               | string         | 播放地址                      |
| categoryIds      | array [int64]                                        | string         | 分类ID列表                    |
| shot             | int                                                  | number/string  | 是否更新截图(0:不更新,1:更新) |
| tagIds           | array [int64]                                        | string         | 标签ID列表                    |
| sort             | int                                                  | number/string  | 内容排序值                    |



> JSON 示例

```json
{
  "repositoryId": "string($int64)",
  "id": "string($int64)",
  "title": "string",
  "description": "string",
  "fromId": "string($int64)",
  "fromType": "WEB | LOCAL | VEGETABLE_MARKET | VCG | GD | QIPING",
  "themeColor": "string",
  "topColor": "string",
  "priClassify": 0,
  "secClassify": "string",
  "version": 0,
  "createdAt": "string($int64)",
  "updatedAt": "string($int64)",
  "type": "TEMPLATE | IMAGE | VIDEO | MUSIC | FONT",
  "preview": {
    "id": "string($int64)",
    "imageUrl": "string",
    "partVideoUrl": "string",
    "videoUrl": "string",
    "width": 0,
    "height": 0,
    "hex": "string",
    "type": "PREVIEW_IMG | COMPOSITE_IMG | EXTEND_IMG | PREVIEW_GIF"
  },
  "compositePreview": {
    "id": "string($int64)",
    "imageUrl": "string",
    "partVideoUrl": "string",
    "videoUrl": "string",
    "width": 0,
    "height": 0,
    "hex": "string",
    "type": "PREVIEW_IMG | COMPOSITE_IMG | EXTEND_IMG | PREVIEW_GIF"
  },
  "extendsPreview": [
    {
      "id": "string($int64)",
      "imageUrl": "string",
      "partVideoUrl": "string",
      "videoUrl": "string",
      "width": 0,
      "height": 0,
      "hex": "string",
      "type": "PREVIEW_IMG | COMPOSITE_IMG | EXTEND_IMG | PREVIEW_GIF"
    }
  ],
  "design": {
    "id": "string($int64)",
    "url": "string",
    "size": "string($int64)",
    "containMaterial": [
      "string"
    ],
    "dpi": "string($int64)",
    "orientation": "HORIZONTAL | VERTICAL",
    "ext": "string"
  },
  "origin": {
    "id": "string($int64)",
    "url": "string",
    "size": "string($int64)",
    "dpi": 0
  },
  "playUrl": "string",
  "categoryIds": [
    "string($int64)"
  ],
  "shot": 0,
  "tagIds": [
    "string($int64)"
  ],
  "sort": 0
}
```



<h3 id="updatecontentbyid"> 修改内容信息 - 部分更新</h3>


* HTTP Gateway
	* URL: `/v1/cmc/content`
	* Method: `PUT`
	* Content-Type: `application/json`

* 请求类型: ***UpdateContentByIdRequest***

>  更新内容信息

| 字段   | protobuf 类型             | json 类型     | 说明                          |
| ------ | ------------------------- | ------------- | ----------------------------- |
| id     | int64                     | string        | id                            |
| title  | string                    | string        | 标题                          |
| design | [DesignInfo](#designinfo) | object        | 设计文件详情                  |
| shot   | int                       | number/string | 是否更新截图(0:不更新,1:更新) |


> JSON 示例

```json
{
  "id": "string($int64)",
  "title": "string",
  "design": {
    "id": "string($int64)",
    "url": "string",
    "size": "string($int64)",
    "containMaterial": [
      "string"
    ],
    "dpi": "string($int64)",
    "orientation": "HORIZONTAL | VERTICAL",
    "ext": "string"
  },
  "shot": 0
}
```



* 返回类型: ***BoolValue***

>  Wrapper message for `bool`.
>
>  The JSON representation for `BoolValue` is JSON `true` and `false`.

| 字段  | protobuf 类型 | json 类型   | 说明            |
| ----- | ------------- | ----------- | --------------- |
| value | bool          | true, false | The bool value. |



> JSON 示例

```json
{
  "value": true
}
```



<h3 id="deletecontentbyid"> 删除内容 - 批量</h3>


* HTTP Gateway
	* URL: `/v1/cmc/content/{id}`
	* Method: `DELETE`
	* Content-Type: `application/json`

* 请求类型: ***DeleteContentByIdRequest***

>  批量删除内容

| 字段 | protobuf 类型 | json 类型 | 说明 |
| ---- | ------------- | --------- | ---- |
| id   | array [int64] | string    | id   |






* 返回类型: ***BoolValue***

>  Wrapper message for `bool`.
>
>  The JSON representation for `BoolValue` is JSON `true` and `false`.

| 字段  | protobuf 类型 | json 类型   | 说明            |
| ----- | ------------- | ----------- | --------------- |
| value | bool          | true, false | The bool value. |

> JSON 示例

```json
{
  "value": true
}
```

********

## *参数与结构体说明*




<h3 id="contentfromtype">ContentFromType</h3>

>  资源来源

* 枚举说明

| 枚举名称 (string) | 枚举数值 (integer) | 说明       |
| ----------------- | ------------------ | ---------- |
| WEB               | 0                  | WEB        |
| LOCAL             | 1                  | 本地客户端 |
| VEGETABLE_MARKET  | 2                  | 菜市场     |
| VCG               | 3                  | 视觉中国,  |
| GD                | 4                  | 稿定       |
| QIPING            | 5                  | 启屏       |


<h3 id="orientationtype">OrientationType</h3>

> 方向

* 枚举说明

| 枚举名称 (string) | 枚举数值 (integer) | 说明 |
| ----------------- | ------------------ | ---- |
| HORIZONTAL        | 0                  | 横屏 |
| VERTICAL          | 1                  | 竖屏 |


<h3 id="previewtype">PreviewType</h3>

>  预览图类型

* 枚举说明

| 枚举名称 (string) | 枚举数值 (integer) | 说明       |
| ----------------- | ------------------ | ---------- |
| PREVIEW_IMG       | 0                  | 预览图     |
| COMPOSITE_IMG     | 1                  | 合成预览图 |
| EXTEND_IMG        | 2                  | 扩展图     |
| PREVIEW_GIF       | 3                  | GIF图      |


<h3 id="repositorycontenttype">RepositoryContentType</h3>

>  内容类型

* 枚举说明

| 枚举名称 (string) | 枚举数值 (integer) | 说明 |
| ----------------- | ------------------ | ---- |
| TEMPLATE          | 0                  | 模板 |
| IMAGE             | 1                  | 图片 |
| VIDEO             | 2                  | 视频 |
| MUSIC             | 3                  | 音频 |
| FONT              | 4                  | 字体 |








<h3 id="contentinfo">ContentInfo</h3>

>  内容详情

* 字段说明

| 字段             | protobuf 类型                                        | json 类型      | 说明                          | 默认值 | 是否必传 |
| ---------------- | ---------------------------------------------------- | -------------- | ----------------------------- | ------ | -------- |
| repositoryId     | int64                                                | string         | 空间ID                        | -      | false    |
| id               | int64                                                | string         | id                            | -      | false    |
| title            | string                                               | string         | 标题                          | -      | false    |
| description      | string                                               | string         | 描述                          | -      | false    |
| fromId           | int64                                                | string         | 来源                          | -      | false    |
| fromType         | enum [ContentFromType](#contentfromtype)             | string/integer | 来源分类                      | -      | false    |
| themeColor       | string                                               | string         | 主题颜色                      | -      | false    |
| topColor         | string                                               | string         | 颜色TOP5                      | -      | false    |
| priClassify      | int                                                  | number/string  | 一级分类（编辑器类型）        | -      | false    |
| secClassify      | string                                               | string         | 二级分类 (编辑器类型)         | -      | false    |
| version          | int                                                  | number/string  | 版本号                        | -      | false    |
| createdAt        | int64                                                | string         | 创建时间                      | -      | false    |
| updatedAt        | int64                                                | string         | 更新时间                      | -      | false    |
| type             | enum [RepositoryContentType](#repositorycontenttype) | string/integer | 类型                          | -      | false    |
| preview          | [PreViewInfo](#previewinfo)                          | object         | 预览图                        | -      | false    |
| compositePreview | [PreViewInfo](#previewinfo)                          | object         | 合成预览图                    | -      | false    |
| extendsPreview   | array [[PreViewInfo](#previewinfo)]                  | array          | 扩展预览图                    | -      | false    |
| design           | [DesignInfo](#designinfo)                            | object         | 设计文件详情                  | -      | false    |
| origin           | [OriginInfo](#origininfo)                            | object         | 源文件                        | -      | false    |
| playUrl          | string                                               | string         | 播放地址                      | -      | false    |
| categoryIds      | array [int64]                                        | string         | 分类ID列表                    | -      | false    |
| shot             | int                                                  | number/string  | 是否更新截图(0:不更新,1:更新) | -      | false    |
| tagIds           | array [int64]                                        | string         | 标签ID列表                    | -      | false    |
| sort             | int                                                  | number/string  | 内容排序值                    | -      | false    |


<h3 id="designinfo">DesignInfo</h3>

>  设计文件

* 字段说明

| 字段            | protobuf 类型                            | json 类型      | 说明     | 默认值 | 是否必传 |
| --------------- | ---------------------------------------- | -------------- | -------- | ------ | -------- |
| id              | int64                                    | string         | id       | -      | false    |
| url             | string                                   | string         | 地址     | -      | false    |
| size            | int64                                    | string         | 文件大小 | -      | false    |
| containMaterial | array [string]                           | string         | 包含素材 | -      | false    |
| dpi             | int64                                    | string         | dpi      | -      | false    |
| orientation     | enum [OrientationType](#orientationtype) | string/integer | 方向     | -      | false    |
| ext             | string                                   | string         | 扩展信息 | -      | false    |


<h3 id="origininfo">OriginInfo</h3>

>  源文件

* 字段说明

| 字段 | protobuf 类型 | json 类型     | 说明     | 默认值 | 是否必传 |
| ---- | ------------- | ------------- | -------- | ------ | -------- |
| id   | int64         | string        | id       | -      | false    |
| url  | string        | string        | 地址     | -      | false    |
| size | int64         | string        | 文件大小 | -      | false    |
| dpi  | int           | number/string | dpi      | -      | false    |


<h3 id="previewinfo">PreViewInfo</h3>

>  资源 - 预览图

* 字段说明

| 字段         | protobuf 类型                    | json 类型      | 说明      | 默认值 | 是否必传 |
| ------------ | -------------------------------- | -------------- | --------- | ------ | -------- |
| id           | int64                            | string         | id        | -      | false    |
| imageUrl     | string                           | string         | 预览图    | -      | false    |
| partVideoUrl | string                           | string         | 短视频URL | -      | false    |
| videoUrl     | string                           | string         | 视频URL   | -      | false    |
| width        | int                              | number/string  | 宽        | -      | false    |
| height       | int                              | number/string  | 高        | -      | false    |
| hex          | string                           | string         | 主色调    | -      | false    |
| type         | enum [PreviewType](#previewtype) | string/integer | 预览类型  | -      | false    |