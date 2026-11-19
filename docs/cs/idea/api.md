# API 与软件接口基础

## 1. 核心概念

| 概念 | 全称 / 含义 | 记忆要点 |
| --- | --- | --- |
| API | Application Programming Interface，应用程序编程接口 | 软件对外提供的功能入口与交互契约 |
| SDK | Software Development Kit，软件开发工具包 | 帮助开发者使用某个平台或 API 的工具集合，常封装请求、认证、数据模型和错误处理 |
| JSON | JavaScript Object Notation | 常见的数据交换格式 |
| REST | Representational State Transfer | 一种常见的 API 架构风格 |
| OpenAPI | OpenAPI Specification | 用 JSON/YAML 描述 HTTP API 的标准 |
| Swagger UI | OpenAPI 生态中的文档展示工具 | 将 OpenAPI 描述渲染成交互式文档，可试调用接口 |

- API 定义“可以调用什么、按什么规则调用”，SDK 提供“更方便调用这些能力的工具”。
- SDK 常基于 API 构建，但并非每个 API 都有 SDK；API 也不局限于 HTTP，**API 是一种协议，关键思想是把一层操作黑箱化，外部调用者只需知道怎么用，怎么调，返回数据是怎样的**。

## 2. 一个 HTTP API 请求由什么组成？

示例：

```http
GET https://api.example.com/v1/videos/123
Authorization: Bearer YOUR_API_KEY
Accept: application/json
```

| 组成 | 含义 | 示例 |
| --- | --- | --- |
| Scheme | 协议 | `https://` |
| Host | 主机 / 域名 | `api.example.com` |
| Base URL | 多个接口共用的基础地址 | `https://api.example.com/v1` |
| Path / Endpoint | 资源路径或具体接口路径 | `/videos/123` |
| HTTP Method | 请求方法 | `GET` |
| Path Parameter | 路径参数，通常标识具体资源 | `/videos/{id}` 中的 `id` |
| Query Parameter | 查询参数，通常用于筛选、排序、分页 | `?page=1&limit=20` |
| Header | 请求头，携带认证、内容类型等元信息 | `Authorization` |
| Request Body | 请求体，通常用于提交数据 | JSON 对象 |

### 常见 HTTP Method

| Method | 常见用途 |
| --- | --- |
| GET | 获取资源 |
| POST | 创建资源或提交操作 |
| PUT | 整体替换资源 |
| PATCH | 部分修改资源 |
| DELETE | 删除资源 |

### Request / Response

- Request（请求）：客户端发给服务器的内容。
- Response（响应）：服务器返回给客户端的内容。
- Response 通常包含 HTTP 状态码、Headers 和 Body。

常见状态码：

| 状态码 | 含义 |
| --- | --- |
| 200 | 成功 |
| 201 | 创建成功 |
| 204 | 成功，无响应内容 |
| 400 | 请求不合法 |
| 401 | 未通过认证 |
| 403 | 没有访问权限 |
| 404 | 资源不存在 |
| 429 | 请求过于频繁 |
| 500 | 服务器内部错误 |
| 503 | 服务暂时不可用 |

## 3. API 文档

API 文档是 API 的使用说明与技术契约，通常说明：

- Base URL、Endpoint、HTTP Method
- Path / Query Parameters
- Headers、认证方式
- Request Body 的字段、类型和约束
- Response 的结构与示例
- 错误码、分页、频率限制等行为

常见载体：

- Markdown / HTML：方便人阅读。
- OpenAPI JSON / YAML：机器可读，可用于生成文档、客户端代码和测试辅助工具。
  - **OpenAPI 与 Swagger：**
  - OpenAPI 是描述 HTTP API 的规范。
  - Swagger 是围绕 OpenAPI 的工具生态；Swagger UI 可展示并试调用接口。

## 4. 常见工程概念

| 概念 | 含义 |
| --- | --- |
| Authentication（认证） | 确认“你是谁” |
| Authorization（授权） | 判断“你能做什么” |
| API Key / Bearer Token | 常见的 API 访问凭证形式 |
| Pagination（分页） | 分批获取大量数据；常见方式有页码分页和游标分页 |
| Rate Limiting（频率限制） | 限制单位时间内的请求数量；超限常返回 `429` |
| Versioning（版本管理） | 例如 `/v1`、`/v2`，用于管理接口演进与兼容性 |
| Error Handling（错误处理） | 通过状态码和结构化错误信息让客户端识别问题 |
| Idempotency（幂等性） | 同一操作重复执行，最终效果与执行一次相同 |
| Webhook | 事件发生时，服务端主动向预先配置的 URL 发送通知 |
| API Gateway | API 网关，常用于统一入口、路由、认证、限流等 |

- API Key / Token 不应泄露在公开前端代码、仓库或日志中。
- GET、PUT、DELETE 按 HTTP 语义具有幂等性（**Idempotency**）；POST 通常不具有。具体业务也可能通过 Idempotency Key 实现重复请求保护：也就是多次重复操作与执行一次的结果一致。
- 重试请求时要考虑网络错误、状态码、退避策略，以及操作是否幂等。

## 5. REST 与 GraphQL

- REST：常以资源为中心，通过多个 Endpoint 和 HTTP Method 表达操作。
- GraphQL：客户端通过 Query / Mutation 声明需要的字段或执行的操作，常通过一个 GraphQL Endpoint 提供服务。
- 两者是不同的 API 设计方式，应根据业务需求选择。

## 6. 前后端分离中的 API

典型关系：

```text
Web / Desktop / Mobile Client
            |
         HTTP API
            |
       Backend Server
            |
         Database
```

- 前端：UI、用户交互。
- 后端：业务逻辑、权限验证、数据处理。
- 数据库：持久化存储。
- API：客户端与服务端之间的通信契约。

同一套后端 API 可以服务多个客户端。提前约定 API 契约，可以让前后端并行开发，减少联调时的字段、参数和行为不一致。

## 7. C# / .NET 中的最小例子

服务端定义 Endpoint：

```csharp
app.MapGet("/api/videos/{id}", (int id) =>
{
    var video = new
    {
        Id = id,
        Title = "Learn Programming",
        Views = 15200
    };

    return Results.Ok(video);
});
```

客户端调用：

```csharp
using System.Net.Http.Json;

var client = new HttpClient();

var video = await client.GetFromJsonAsync<Video>(
    "https://localhost:5001/api/videos/123"
);

public class Video
{
    public int Id { get; set; }
    public string Title { get; set; }
    public int Views { get; set; }
}
```

- `HttpClient`：发送 HTTP 请求。
- `GetFromJsonAsync<T>`：发送 GET 请求并将 JSON 反序列化为 C# 对象。
- `Video`：客户端用于承接响应数据的数据模型。

- [curl](https://curl.se/)：命令行请求工具。

快速测试：

```bash
curl https://api.example.com/v1/videos/123 \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 一句话总结

- API：定义软件之间如何交互。
- OpenAPI：描述 HTTP API 契约。
- Swagger UI：展示和试调用 API 文档。
- SDK：降低开发者调用 API 的成本。
- REST：设计 API 的一种常见架构风格。
```
