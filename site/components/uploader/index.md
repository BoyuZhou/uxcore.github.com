# Uploader

- category: Components
- chinese: 文件上传
- order: 14
- subtype: 表单及相关

---

上传组件, 封装[UploadCore](https://github.com/uxcore/uxcore-uploadcore/)核心组件, 作为UI层.

## API

### reset() 重置文件队列

## Props

| name               | type          | default | Since Ver. |  description |
|----------          |---------------|---------|------------|------------|
|className           |               |         |            | |
|locale              | string        | zh-cn   | 1.1.10     | 国际化，目前支持 `zh-cn` 和 `en-us`|
|fileList            | array         | []      | 1.2.3      |用于展示的文件列表|
|core                | string/`Core` | null    |            | 唯一标识或者UploadCore对象, 防止重复创建, 当传入UploadCore对象时,下列参数和事件设置均无效 |
|name                | string        | 'file'  |            | 上传文件字段名称 |
|url                 | string        | ''      |            | 响应上传服务器地址 |
|params              | object/array  | null    |            | 上传文件额外参数 |
|headers             | array         | null    |            | 上传文件额外头 |
|withCredentials     | bool          | false   |            | 上传文件是否自动附带cookie等信息 |
|timeout             | int           | 0       |            | 上传超时限制 0表示不限制 |
|chunkEnable         | bool          | false   |            | 是否允许分片上传 |
|chunkSize           | size          | 0       |            | 文件分片大小, 默认单位b，0不分片 |
|chunkRetries        | int           | 0       |            | 文件分片上传重试次数 |
|chunkProcessThreads | int           | 2       |            | 分片上传并发数 |
|processThreads      | int           | 2       |            | 文件上传并发数 |
|queueCapcity        | int           | 0       |            | 队列容量，0无限 |
|autoPending         | bool          | true    |            | 是否选择后自动等待上传 |
|multiple            | bool          | true    |            | 是否多选 | 
|accept              | string/array  | null    |            | 允许文件类型 |
|sizeLimit           | size          | 0       |            | 文件大小限制, 0表示不限制 |
|preventDuplicate    | bool          | false   |            | 是否防止文件重复 |

### fileList 的最小格式

```javascript
[
    {
        url: xxx,  // 文件链接，必填
        name: xxx, // filename，必填 
        canRemove: true, // 是否可以删除，可选
        downloadUrl: 'xxxx', // 下载 URL，可选
    }
]

```

### Events

| name     | arguments    | description      |
|----------|--------------|------------------|
| onChange | fileList     | 在上传成功或文件移除后触发，返回文件队列，包括自己传入的`fileList` |
| onCancel | file         | 文件移除后触发，上传的文件和默认列表的文件格式会有所不同，文件格式参见下面的 fileList 格式|
| onfileuploaderror | `File`, `Error` | 文件上传失败 | 


### fileList 的格式
```javascript
[
    // 上传后的文件的格式， responce 即服务器返回的值
    {
        type: 'upload',
        ext: file.ext,
        name: file.name,
        response: JSON.parse(file.response.rawResponse.rawResponse)
    },
    // 预览用文件的格式， `props.fileList` 相关， responce 即 `props.fileList` 里传入的格式。
    {
        type: 'list',
        response: file
    }
]
```



### Other Events

| name     | arguments    | description      |
|----------|--------------|------------------|
|onqueueuploadstart | | 队列上传开始 |
|onqueueuploadend | | 队列上传结束 |
|onqueuefileadded | `File` | 队列添加了一个文件 |
|onqueuefilefiltered | `File`, `Error` | 队列过滤了一个文件 |
|onqueueerror | `Error` | 队列错误 |
|onstatchange | `Stat` | 文件统计发生变化 |
|onfileuploadstart | `File` | 文件上传开始 |
|onfileuploadpreparing | `FileRequest` | 文件上传准备时 |
|onfileuploadprepared | `File`, `FileRequest` | 文件上传准备好了 |
|onchunkuploadpreparing | `ChunkRequest` |  分块上传准备时 |
|onchunkuploadcompleting | `ChunkResponse` |  分块上传结束时 |
|onfileuploadprogress | `File`, `Progress` | 文件上传进度中 |
|onfileuploadend | `File` | 文件上传结束 |
|onfileuploadcompleting | `FileResponse` |  文件上传结束时 |
|onfileuploadsuccess | `File`, `FileResponse` | 文件上传成功 |
|onfileuploadcompleted | `File`, `Status`| 文件上传完成了 |
|onfilestatuschange | `File`, `Status` | 文件状态发生变化 |
|onfilecancel | `File` | 文件退出 |


具体配置信息见<https://github.com/uxcore/uxcore-uploadcore/blob/master/README.md>.
