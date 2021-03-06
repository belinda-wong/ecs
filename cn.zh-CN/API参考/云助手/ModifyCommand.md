# ModifyCommand {#ModifyCommand .reference}

修改一条云助手命令相关参数以及命令内容。

## 描述 {#section_s4q_vr4_ydb .section}

-   命令执行期间也允许修改，修改命令后，后续执行会按照新的命令内容执行。
-   您不能修改命令的类型，例如，如果命令是 Shell 命令（`RunShellScript`），则不能修改为 Bat 命令（`RunBatScript`）。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyCommand|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|CommandId|String|是|命令 ID。您可以通过接口 [DescribeCommands](cn.zh-CN/API参考/云助手/DescribeCommands.md#) 查询所有可用的 `CommandId`。|
|Name|String|否|命令名称，支持全字符集。|
|Description|String|否|命令描述，支持全字符集。|
|WorkingDir|String|否|命令将在实例中的什么路径下执行。默认值：-   对于 Linux 实例，默认在管理员 root 用户的 home 目录下，具体为 `/root` 目录。
-   对于 Windows 实例，默认在 [云助手客户端](../cn.zh-CN/产品简介/云助手/云助手客户端.md#) 进程所在目录，例如，`C:\ProgramData\aliyun\assist\$(version)`。

|
|TimeOut|Integer|否|修改命令在 ECS 实例中执行时最大的超时时间，单位为秒。当因为某种原因无法运行您创建的命令时，会出现超时现象；超时后，云助手客户端会强制终止命令进程，即取消命令的 PID。参数取值必须大于等于 `60`，如果取值小于 `60`，默认为 60 秒。默认值：3600

|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyCommand
&RegionId=cn-hangzhou
&CommandId=c-e996287206324975b5fbe1dxxxxxxxxx
&NameId=Test
&TimeOut=120
&<公共请求参数>
```

**正常返回示例** 

**XML 格式**

```
<ModifyCommandResponse>
    <RequestId>540CFF28-407A-40B5-B6A5-73Bxxxxxxxxx</RequestId>
</ModifyCommandResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"540CFF28-407A-40B5-B6A5-73Bxxxxxxxxx",
}
```

**异常返回示例** 

**XML 格式**

```
<Error>
    <RequestId>540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>InvalidInstance.NoClient</Code>
    <Message>The specified instances have no cloud assistant client installed.</Message>
</Error>
```

 **JSON 格式** 

```
{
    "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
    "HostId": "ecs.aliyuncs.com"
    "Code": "InvalidInstance.NoClient"
    "Message": "The specified instances have no cloud assistant client installed."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter.CommandId|The input parameter “CommandId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `CommandId`。|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `RegionId`，或者您暂时不能使用指定 `RegionId` 里的资源。|
|InvalidCmdId.NotFound|The specified CommandId does not exist.|404|指定的 `CommandId` 不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的 `RegionId` 不存在。|
|InternalError.Dispatch|An internal error occurred when dispath the request|500|内部错误，请稍后尝试。|

