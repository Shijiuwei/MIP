# 为 public-apis 做出贡献

> 虽然我们非常感谢大量的拉取请求（Pull Requests）和社区参与，但有些拉取请求是专门为了推销提供付费解决方案的公司 API 而发起的。本 API 列表并非营销工具，而是一个帮助社区快速、轻松地构建应用程序并使用免费公共 API 的工具。任何被认定为营销推广企图的拉取请求都将不予接受。
>
> 在提交之前，请确保您想要添加的 API 具有完全免费的访问权限，或至少提供免费套餐（Free Tier），且不依赖于购买特定硬件设备或付费服务。一个会被拒绝的例子是用于控制智能插座的 API——虽然该 API 本身是免费的，但您必须先购买该智能硬件设备才能使用。
>
> 感谢您的理解！ :)

## 格式规范

当前的 API 条目格式如下：

| API | Description | Auth | HTTPS | CORS | Call this API |
| --- | --- | --- | --- | --- | --- |
| API 标题（API 文档链接） | API 的简短描述 | 该 API 是否需要身份验证？ \* | 该 API 是否支持 HTTPS？ | 该 API 是否支持 [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)？ \* | [该 API 是否有公开的 Postman 集合？](https://learning.postman.com/docs/publishing-your-api/run-in-postman/creating-run-button/) |

条目示例：

```
| [NASA](https://api.nasa.gov) | NASA data, including imagery | No | Yes | Yes | [Run in Postman Button]
```

\* 目前，`Auth`（认证）字段仅接受以下输入值：

* `OAuth` - _该 API 支持 OAuth 认证_
* `apiKey` - _该 API 使用私有密钥字符串/令牌进行认证——请尽量使用正确的参数名称_
* `X-Mashape-Key` - _可能需要发送的请求头（Header）名称_
* `No` - _该 API 无需任何身份验证即可运行_
* `User-Agent` - _向该 API 发送请求时需要附带的请求头名称_

\* 目前，`CORS`（跨域资源共享）字段仅接受以下输入值：

* `Yes` - _该 API 支持 CORS_
* `No` - _该 API 不支持 CORS_
* `Unknown` - _尚不清楚该 API 是否支持 CORS_

\* 对于 `Call this API`（调用此 API）列，请添加一个指向 Postman 集合的链接。您可能需要先[创建一个集合](https://learning.postman.com/docs/getting-started/first-steps/creating-the-first-collection/)才能生成“Run in Postman”按钮。

_如果没有正确的 [CORS 配置](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)，该 API 将只能在服务器端使用。_

在您 Fork 的仓库中创建分支并完成修改后，就可以[发起拉取请求（Pull Request）][pr-link]了。

*向 Public APIs 提交拉取请求时，请遵循以下指南*

## MCP 服务器

[模型上下文协议（Model Context Protocol）](https://modelcontextprotocol.io) 服务器与 REST API 分开列出，位于 [MCP Servers](README.md#mcp-servers) 章节中。它们使用不同的条目格式：MCP 服务器是安装到客户端中运行，而不是通过 HTTP 调用的，因此 `HTTPS` 和 `CORS` 不适用于它。

当前的 MCP 条目格式如下：

| Name | Description | Auth | Transport | Install |
| --- | --- | --- | --- | --- |
| 服务器名称（仓库或文档链接） | 服务器的简短描述 | 是否需要身份验证？ \* | 支持哪些传输方式？ \* | 哪些应用市场收录了它？ \* |

条目示例：

````
| [Filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) | Read/write local files | No | `stdio` | – |
````

\* `Auth` 字段使用与上述 API 表格相同的允许输入值：`OAuth`、`apiKey`、`X-Mashape-Key`、`No`、`User-Agent`。

\* 目前，`Transport`（传输方式）字段仅接受以下输入值：

* `stdio` - _服务器通过标准输入/输出作为本地子进程运行_
* `HTTP` - _服务器可通过流式 HTTP（Streamable HTTP）访问_
* `SSE` - _服务器使用传统的服务器发送事件（Server-Sent Events）传输方式_

如果您的服务器支持多种传输方式，请用英文逗号分隔，例如 `` `stdio`, `HTTP` ``。

\* 对于 `Install`（安装）字段，请链接到您的服务器实际发布的应用市场页面，并使用 ` · ` 分隔。我们目前追踪 [Cursor](https://cursor.directory)、[Anthropic](https://claude.ai/directory) 和 [Glama](https://glama.ai/mcp/servers)。如果尚未在任何地方上架，请使用 `–` —— 这是正常状态，不会产生任何负面影响。

**请仅链接到真实存在的上架页面。** 指向返回 404 错误的应用市场页面链接将导致您的拉取请求被直接关闭。

## 拉取请求（Pull Request）指南

* 切勿添加已收录 API 的更新版本或新版本；旧版本的 API 会被弃用并替换。
* 请继续遵循每个分类章节中现有的字母顺序排列。
* 表格的每一列两侧都应各留一个空格进行填充。
* 描述（Description）长度不得超过 100 个字符。
* 如果某个 API 似乎属于多个类别，请将其放在与该 API 所提供核心服务最契合的分类中。例如，Instagram API 被列在 `Social`（社交）下，因为它主要是一个社交网络，尽管它也适用于 `Photography`（摄影）。
* 每个拉取请求仅添加一个链接。
* 确保 PR 标题采用 `Add Api-name API` 的格式，*例如*：`Add Blockchain API`。
* 使用简短且具描述性的提交信息（Commit Message），*例如*：❌ `Update Readme.md` ✔ `Add Blockchain API to Cryptocurrency`。
* 在创建新的拉取请求之前，请先搜索过往的 Pull Requests 或 Issues，以免提交重复内容。
* 不要在 API 名称中包含顶级域名（TLD），*例如*：❌ Gmail.com ✔ Gmail。
* 请确保 API 名称不以 `API` 结尾，*例如*：❌ Gmail API ✔ Gmail。
* 请确保该 API 拥有完善的官方文档。
* 在发起拉取请求之前，请务必将所有提交（Commits）压缩合并（Squash）为一个提交。如果在代码审查（Review）后需要修改，也请务必将所有新增的提交压缩合并在一起。[此 Wiki 页面][squash-link]详细介绍了压缩合并的流程。
* 将您的拉取请求目标分支指向 `public-apis` 仓库的 `master` 分支。

提交拉取请求后，项目协作者将审查您提议的更改，并决定是否采纳（合并）您的贡献。

### 拉取请求实用技巧

* [Fork][fork-link] 本仓库并将其[克隆（Clone）][clone-link]到本地。通过将原始 `upstream` 仓库添加为[远程仓库（Remote）][remote-link]，将您的本地仓库与原仓库关联起来。经常从 `upstream` 拉取最新更改以保持同步，这样在您提交拉取请求时就不太可能出现合并冲突。请参阅[此处][syncing-link]的详细操作说明。
* 为您的修改创建一个新[分支（Branch）][branch-link]。
* 按照上述项目代码风格进行贡献。这将使协作者更容易合并您的代码，也方便其他人在未来理解和维护。

### 已开启的拉取请求

一旦您开启了拉取请求，围绕您提议的更改就会展开讨论。

其他贡献者和用户可能会发表意见，但最终决定权由项目协作者掌握。

在讨论过程中，您可能会被要求对拉取请求进行一些修改。

如果是这样，请向您的分支添加更多提交并推送——它们将自动同步到现有的拉取请求中。但别忘了将它们压缩合并（Squash）。

开启拉取请求将触发自动构建，以检查项目中所有链接的有效性。构建完成后，**请确保构建已通过**。如果构建未通过，请查看构建日志并修正您贡献中发现的任何错误。

*感谢您成为本项目的一员，我们期待尽快收到您的贡献！*

[branch-link]: <http://guides.github.com/introduction/flow/>
[clone-link]: <https://help.github.com/articles/cloning-a-repository/>
[fork-link]: <http://guides.github.com/activities/forking/>
[oauth-link]: <https://en.wikipedia.org/wiki/OAuth>
[pr-link]: <https://help.github.com/articles/creating-a-pull-request/>
[remote-link]: <https://help.github.com/articles/configuring-a-remote-for-a-fork/>
[syncing-link]: <https://help.github.com/articles/syncing-a-fork>
[squash-link]: <https://github.com/todotxt/todo.txt-android/wiki/Squash-All-Commits-Related-to-a-Single-Issue-into-a-Single-Commit>