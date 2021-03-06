## 1. 接口描述

域名：monitor.api.qcloud.com
接口：GetMonitorData

查询文档数据库MongoDB产品监控数据，入参取值如下：
namespace: qce/cmongo
维度名称固定取值：target
dimensions.0.name=target
dimensions.0.value=视查询维度而定

下面来说明下dimensions.0.value的取值。
腾讯云提供的MongoDB是集群服务，通过本API可以查询“整个集群”、“某个副本集”、“某个节点”三个维度的监控数据。
其中：
“整个集群”代表了您所购买的某一个MongoDB实例，这个维度可以查询整个实例的读写请求次数、容量使用率、超时请求等。
“某个副本集”维度可查询集群下的某一个副本集内部的容量使用率和主从延迟。副本集实例本身只包含一个副本集，分片实例的每一片都是一个副本。
“某个节点”维度可以查询集群内的任意节点的CPU、内存等信息。

dimensions.0.value 取值参照表

| 取值类型  | 取值示例                                     | 描述                                       |
| ----- | ---------------------------------------- | ---------------------------------------- |
| 实例ID  | cmgo-6ielucen                            | 实例ID一个MongoDB实例的唯一标识；可以在[MongoDB控制台](https://console.cloud.tencent.com/mongodb)查询到；或者调用MognoDB的API也可以获取 |
| 副本集ID | cmgo-6ielucen_0cmgo-6ielucen_2           | 在实例ID后面拼接 “_索引号”可以得到副本集ID；“索引号”从0开始，最大值为副本集个数-1；副本集实例只有一个副本集，所以固定拼接“_0”即可；分片实例有多个片，每一片都是副本集，举例：第3个片的副本集ID就是拼接“_2” |
| 节点ID  | cmgo-6ielucen_0-node-primarycmgo-6ielucen_1-node-slave0cmgo-6ielucen_3-node-slave2 | 在副本集ID后面拼接“-node-primary”得到该副本集的主节点ID；拼接“-node-slave从节点索引号”可得到对应的从节点的ID，“从节点索引号”从0开始，最大值为从节点个数-1 |

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href="/doc/api/405/公共请求参数" title="公共请求参数">公共请求参数</a>页面。其中，此接口的Action字段为GetMonitorData。

### 2.1输入参数

| 参数名称               | 必选   | 类型       | 输入内容    | 描述                                       |
| ------------------ | ---- | -------- | ------- | ---------------------------------------- |
| namespace          | 是    | String   | qce/cvm | 命名空间，每个云产品会有一个命名空间，具体名称见输入内容一栏。          |
| metricName         | 是    | String   | 具体的指标名称 | 指标名称，具体名称见2.2                            |
| dimensions.0.name  | 是    | String   | target  | 入参为target                                |
| dimensions.0.value | 是    | String   | 视查询维度而定 | 请参考1.接口描述中value取值参照表                     |
| period             | 否    | Int      | 60/300  | 监控统计周期，绝大部分指标支持60s统计粒度，部分指标仅支持300s统计粒度，统计粒度根据指标的不同而变。输入参数时可参考2.2的指标详情列表。 |
| startTime          | 否    | Datetime | 起始时间    | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| endTime            | 否    | Datetime | 结束时间    | 结束时间，默认为当前时间。 endTime不能小于startTime       |
### 2.2 指标名称

| 指标                | 含义                       | 单位   | 集群/实例 | dimensions.0.value取值 |
| ----------------- | ------------------------ | ---- | ----- | -------------------- |
| inserts           | 单位时间内写入次数                | 次    | 集群/实例 | 实例ID                 |
| reads             | 单位时间内读取次数                | 次    | 集群/实例 | 实例ID                 |
| updates           | 单位时间内更新次数                | 次    | 集群/实例 | 实例ID                 |
| deletes           | 单位时间内删除次数                | 次    | 集群/实例 | 实例ID                 |
| counts            | 单位时间内ount次数              | 次    | 集群/实例 | 实例ID                 |
| aggregates        | 单位时间内aggregates次数        | 次    | 集群/实例 | 实例ID                 |
| cluster_diskusage | 集群容量使用率                  | %    | 集群/实例 | 实例ID                 |
| success           | 单位时间内成功请求次数              | 次    | 集群/实例 | 实例ID                 |
| delay_10          | 单位时间内成功请求延迟在10ms-50ms次数  | 次    | 集群/实例 | 实例ID                 |
| delay_50          | 单位时间内成功请求延迟在50ms-100ms次数 | 次    | 集群/实例 | 实例ID                 |
| delay_100         | 单位时间内成功请求延迟在100ms以上次数    | 次    | 集群/实例 | 实例ID                 |
| replica_diskusage | 副本集容量使用率                 | %    | 副本集   | 副本集ID                |
| slavedelay        | 主从单位时间内平均延迟              | 秒    | 副本集   | 副本集ID                |
| cpuusage          | CPU使用率                   | %    | 节点    | 节点ID                 |
| memusage          | 内存使用率                    | %    | 节点    | 节点ID                 |
| qr                | Read请求等待队列中的个数           | 个    | 节点    | 节点ID                 |
| qw                | Write请求等待队列中的个数          | 个    | 节点    | 节点ID                 |
| conn              | 连接数                      | 个    | 节点    | 节点ID                 |
| netin             | 网络入流量                    | MB/s | 节点    | 节点ID                 |
| netout            | 网络出流量                    | MB/s | 节点    | 节点ID                 |


## 3. 输出参数

| 参数名称       | 类型       | 描述                  |
| ---------- | -------- | ------------------- |
| code       | Int      | 错误码, 0: 成功, 其他值表示失败 |
| message    | String   | 返回信息                |
| startTime  | Datetime | 起始时间                |
| endTime    | Datetime | 结束时间                |
| metricName | String   | 指标名称                |
| period     | Int      | 监控统计周期              |
| dataPoints | Array    | 监控数据列表              |


## 4. 错误码表

| 错误代码 | 错误描述    | 英文描述                                 |
| ---- | ------- | ------------------------------------ |
| -502 | 资源不存在   | OperationDenied.SourceNotExists      |
| -503 | 请求参数有误  | InvalidParameter                     |
| -505 | 参数缺失    | InvalidParameter.MissingParameter    |
| -507 | 超出限制    | OperationDenied.ExceedLimit          |
| -509 | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513 | DB操作失败  | InternalError.DBoperationFail        |

## 5. 示例

### 5.1查询某个集群/实例大于100ms的请求数

输入

```
https://monitor.api.qcloud.com/v2/index.php?
&<<a href="https://cloud.tencent.com/doc/api/229/6976">公共请求参数</a>>
&namespace=qce/cmongo
&metricName=delay_100
&dimensions.0.name=target
&dimensions.0.value=cmgo-6ielucen
&startTime=2017-01-09 20:22:00
&endTime=2017-01-09 20:38:00
```

输出

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "metricName": "delay_100",
    "startTime": "2017-01-09 20:20:00",
    "endTime": "2017-01-09 20:35:00",
    "period": 300,
    "dataPoints": [
        257,
        1399,
        2272
    ]
}
```
### 5.2查询某个副本集的主从延时

输入

```
https://monitor.api.qcloud.com/v2/index.php?
&<<a href="https://cloud.tencent.com/doc/api/229/6976">公共请求参数</a>>
&namespace=qce/cmongo
&metricName=slavedelay
&dimensions.0.name=target
&dimensions.0.value=cmgo-6ielucen_0
&startTime=2017-01-09 20:22:00
&endTime=2017-01-09 20:38:00
```

输出

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "metricName": "slavedelay",
    "startTime": "2017-01-09 20:20:00",
    "endTime": "2017-01-09 20:35:00",
    "period": 300,
    "dataPoints": [
        0,
        1,
        0
    ]
}
```
### 5.3查询某个节点的连接数

输入

```
https://monitor.api.qcloud.com/v2/index.php?
&<<a href="https://cloud.tencent.com/doc/api/229/6976">公共请求参数</a>>
&namespace=qce/cmongo
&metricName=slavedelay
&dimensions.0.name=target
&dimensions.0.value=cmgo-6ielucen_0
&startTime=2017-01-09 20:22:00
&endTime=2017-01-09 20:38:00
```

输出

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "metricName": "conn",
    "startTime": "2017-01-09 20:20:00",
    "endTime": "2017-01-09 20:35:00",
    "period": 300,
    "dataPoints": [
        75,
        77,
        79,
        79
    ]
}
```

