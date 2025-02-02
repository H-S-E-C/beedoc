---
name: 发布版本
sort: 2
---
# beego 2.0.2

[Change Log](https://github.com/beego/beego/releases/tag/v2.0.2-beta.1)

# beego 2.0.1

发布2.0.0的时候，因为go mod的一些错误，导致我们 checksum 不再正确，所以发了2.0.1。

# beego 2.0.0

### Refactor
1. 重新将Beego划分成四个主要部分：
   1.1 server: 包括web模块.
   1.2 client: 包括ORM, cache, httplib 模块.
   1.3 task: 支持周期任务和定时任务。
   1.4 core: 包括 validation, config, logs 和 admin 模块.
2. 增加 `adapter` 模块，作为 1.x 升级到 2.x 的适配模块
3. 为 `cache`, `httplib`, `session`, `task`,  `ORM` 模块的 API 增加 `context.Context` .
4. 为 `cache`, `httplib`, `session`, `task`的 API增加 `error` 作为返回值.
5. 解耦各个模块，使各个模块只依赖于 core 模块.
6. 更好的可观测性支持，目前支持了 ORM, web, httplib 模块.
7. 引入 `filter-chain` 模式用于扩展 AOP 业务逻辑.

### Feature:
1. 健康检查能够返回json串了. [4055](https://github.com/beego/beego/pull/4055)
2. TLS 支持 `ClientAuth` 选项了. [4116](https://github.com/beego/beego/pull/4116)
3. `orm.RawSeter` 支持 `orm.Fielder` 接口了. [4191](https://github.com/beego/beego/pull/4191)
4. 支持新的，MySQL的大小写敏感(strict case-sensitive)的操作符. [4198](https://github.com/beego/beego/pull/4198)
5. 在 ORM 中支持 `opentracing` 和 `prometheus`. [4141](https://github.com/beego/beego/pull/4141)
6. 在`httplib`中支持 `prometheus`. [4145](https://github.com/beego/beego/pull/4145)
7. 使用新的API来替换部分过期 `redis` API，同时支持了更加丰富的 `redis` 参数 [4137](https://github.com/beego/beego/pull/4137)
8. `orm`全面支持默认值. [4156](https://github.com/beego/beego/pull/4156)
9. 为`config`模块添加 `Unmarshaler`, `Sub`, `OnChange`方法. [4175](https://github.com/beego/beego/pull/4175)
10. 支持自定义日期格式. [4174](https://github.com/beego/beego/pull/4174), [4179](https://github.com/beego/beego/pull/4179), [4188](https://github.com/beego/beego/pull/4188)
11. 支持时间精度. [4186](https://github.com/beego/beego/pull/4186)
12. 支持 `etcd` 作为配置中心. [4195](https://github.com/beego/beego/pull/4195)
13. 优化 `rawSet.QueryRows`，以避免重复调用`parseStructTag`. [4210](https://github.com/beego/beego/pull/4210)
14. 执行 `ORM` 的命令时，允许忽略部分表. [4211](https://github.com/beego/beego/pull/4211)
15. 支持 `PostgresQueryBuilder` [4205](https://github.com/beego/beego/pull/4205)
16. 强大的自定义日期格式实现`PatternLogFormatter`.[4229](https://github.com/beego/beego/pull/4229)
17. 支持自定义`ES`索引名字. [4233](https://github.com/beego/beego/pull/4233)
18. 支持多server. [4234](https://github.com/beego/beego/pull/4234)
19. 支持 toml. [4262](https://github.com/beego/beego/pull/4262)
20. 使用`unmarshaler`方法以解析`web`中的配置 [4266](https://github.com/beego/beego/pull/4266)
21. 增加`MaxUploadFile`以控制上传文件的内存占用. [4275](https://github.com/beego/beego/pull/4275)
22. 支持使用`json`来初始化`session`实现. [4277](https://github.com/beego/beego/pull/4277)
23. 支持直接使用`config`来读取配置. [4278](https://github.com/beego/beego/pull/4278)
24. `session`支持`CookieSameSite`选项 [4226](https://github.com/beego/beego/pull/4226)

### Fix:
1. 修复`log`重连问题(logs/conn.go). [4056](https://github.com/beego/beego/pull/4056)
2. 请求体过大能正确返回413错误了. [4058](https://github.com/beego/beego/pull/4058)
3. 修复`session`模块`index out of range`错误. [4068](https://github.com/beego/beego/pull/4068)
4. 修复`context/input#Query`方法并发问题. [4066](https://github.com/beego/beego/pull/4066)
5. 允许使用环境变量来指定初始化配置文件. [4111](https://github.com/beego/beego/pull/4111)
6. 为XSRF增加了 httponly 和 secure 的 flag. [4126](https://github.com/beego/beego/pull/4126)
7. 修复了 windows 下创建临时文件的问题 [4244](https://github.com/beego/beego/pull/4244)
8. 主键是非数字类型时，插入时会返回特定的error信息，表明无法生成自增主键. [4150](https://github.com/beego/beego/pull/4150)
9. 修复了`Fielder`在使用`orm.Raw()`的时候，未曾调用`SetRaw`设置值的问题. [4160](https://github.com/beego/beego/pull/4160)
10. 修复在非数字主键下，执行`InsertOrUpdate`方法成功却又返回 error 的问题. [4158](https://github.com/beego/beego/pull/4158)
11. 修复字段是结构体的情况下，`queryRaw`未能正确赋值结果集的问题 [4173](https://github.com/beego/beego/pull/4173)
12. `validator.Error`在缺省tag信息的情况下，会使用字段名字来构建错误信息. [4225](https://github.com/beego/beego/pull/4225)
13. 修复task模块的死锁问题. [4246](https://github.com/beego/beego/pull/4246)
14. 修复http提交表单过大导致OOM的问题. [4272](https://github.com/beego/beego/pull/4272)

### Doc:
1. 修复一些错别字。[4251](https://github.com/beego/beego/pull/4251), [4135](https://github.com/beego/beego/pull/4135), [4107](https://github.com/beego/beego/pull/4107)

# beego 1.12.3

### Feature:
1. 健康检查可以返回 JSON 格式数据. [4055](https://github.com/beego/beego/pull/4055)
2. TLS 支持`ClientAuth`选项. [4116](https://github.com/beego/beego/pull/4116)
3. `orm.RawSeter`支持 `orm.Fielder`. [4191](https://github.com/beego/beego/pull/4191)
4. 支持MySQL字符串敏感操作符. [4198](https://github.com/beego/beego/pull/4198)

### Fix:
1. 修复重连BUG logs/conn.go. [4056](https://github.com/beego/beego/pull/4056)
2. 请求过大时返回403错误码. [4058](https://github.com/beego/beego/pull/4058)
3. 修复Prepare Statement中的多线程竞争. [4061](https://github.com/beego/beego/pull/4061)
4. 修复Session中`index out of range`错误. [4068](https://github.com/beego/beego/pull/4068)
5. 修复context/input Query的并发问题. [4066](https://github.com/beego/beego/pull/4066)
6. 允许使用环境变量来指定配置文件. [4111](https://github.com/beego/beego/pull/4111)
7. XSRF添加 secure 和 http only 标志. [4126](https://github.com/beego/beego/pull/4126)
8. 修复Windows下临时文件目录错误问题 [4244](https://github.com/beego/beego/pull/4244)
9. 支持CookieSameSite选项. [4226](https://github.com/beego/beego/pull/4226)
10. 减小`Prepare Statement`缓冲的大小，避免`too many statement`错误. [4261](https://github.com/beego/beego/pull/4261)

# beego 1.12.2
1. Fix: 热更新老进程未能退出问题 [#4005](https://github.com/beego/beego/pull/4005)
2. Enhance: ORM异常退出时打印堆栈 [#3743](https://github.com/beego/beego/pull/3743)
3. Enhance: GetMapData使用读锁 [#3803](https://github.com/beego/beego/pull/3803)
4. Fix: 正确读取符号路径目录下的文件 [#3818](https://github.com/beego/beego/pull/3818)
5. Fix: Cache, context, session使用锁来保护变量 [#3922](https://github.com/beego/beego/pull/3922)
6. Fix: URL编码的路径被错误解码导致匹配路径错误 [#3943](https://github.com/beego/beego/pull/3943)
7. Fix: genRouterCode生成错误代码 [#3981](https://github.com/beego/beego/pull/3981)
8. Enhance: 静态文件缓存使用LRU算法，并且限制文件数量和文件大小 [#3984](https://github.com/beego/beego/pull/3984)
9. Fix: 设置最大连接数失效问题 [#3985](https://github.com/beego/beego/pull/3985)
10. Fix: SQLite 不支持SELECT ... FOR UPDATE [#3992](https://github.com/beego/beego/pull/3992)
11. Enhance: 为`httplib`的`PostFile`方法添加`Transfer-Encoding` [#3993](https://github.com/beego/beego/pull/3993)
12. Enhance: ORM支持位操作 [#3994](https://github.com/beego/beego/pull/3994)
13. Fix: `BConfig.Listen.Graceful`为`true`的时候`RunWithMiddleware`,`App.Run(middleware)`不起效 [#3995](https://github.com/beego/beego/pull/3995)
14. Fix: 错误信息中带上`label` [#4001](https://github.com/beego/beego/pull/4001)
15. Fix: 关闭`logger`之后依旧发送关闭信号，造成 panic [#4004](https://github.com/beego/beego/pull/4004)
16. Enhance: 在`beforeFilter`执行之前设置好`RouterPattern` [#4007](https://github.com/beego/beego/pull/4007)
17. Fix: 使用`HTMLEscapeString`以避免 XSS 攻击 [#4018](https://github.com/beego/beego/pull/4018)
18. Fix: 进程未能退出 [#4005](https://github.com/beego/beego/pull/4005)
19. Enhance: 使用`scan`指令取代`keys` [#4016](https://github.com/beego/beego/pull/4016)
20. Feature: 支持`prometheus` [#4021](https://github.com/beego/beego/pull/4021)
21. Fix: `Prepare Statement`数量超出数据库上限 [#4025](https://github.com/beego/beego/pull/4025)
22. Enhance: 支持全网段手机号码校验 [#4027](https://github.com/beego/beego/pull/4027)
23. Fix: 无法设置`section`的名字 [#4027](https://github.com/beego/beego/pull/4027)
24. Fix: 当`multi`为 0 时`orm/db.go`中`strings.Repeat`会 panic  [#4032](https://github.com/beego/beego/pull/4032)
25. Enhance: `redis`的 `idle timeout`可配置化 [#4033](https://github.com/beego/beego/pull/4033)

# beego 1.10.0
1. Update log.go add GetLevel Function to Log [#2970](https://github.com/beego/beego/pull/2970)
2. Fix a typo "conflict" [#2971](https://github.com/beego/beego/pull/2971)
3. Bug on private fields [#2978](https://github.com/beego/beego/pull/2978)
4. Fix access log console unexpected '\n' at end of each log. [#2976](https://github.com/beego/beego/pull/2976)
5. Fix Documentation for HTTP status codes descriptions. [#2992](https://github.com/beego/beego/pull/2992)
6. Redis cache: make MaxIdle configurable [#3004](https://github.com/beego/beego/pull/3004)
7. Update: Fix migration generate SQL [#3017](https://github.com/beego/beego/pull/3017)
8. Handle pointer validation [#3046](https://github.com/beego/beego/pull/3046)
9. Fix the issue TaseCase TestFormatHeader_0 is failed [#3066](https://github.com/beego/beego/pull/3066)
10. Fix BEEGO_RUNMODE [#3064](https://github.com/beego/beego/pull/3064)
11. Swagger: Allow example values with different types, allow example for enum. [#3085](https://github.com/beego/beego/pull/3085)
12. Fix the bug: unable to add column with ALTER TABLE [#2999](https://github.com/beego/beego/pull/2999)
13. Set default Beego RunMode to production [#3076](https://github.com/beego/beego/pull/3076)
14. Fix typo [#3103](https://github.com/beego/beego/pull/3103)
15. In dev mode, template parse error cause program lock [#3126](https://github.com/beego/beego/pull/3126)
16. Amend a very minor typo in a variable name [#3115](https://github.com/beego/beego/pull/3115)
17. When log maxSize set big int，FileWrite Init fail [#3109](https://github.com/beego/beego/pull/3109)
18. Change github.com/garyburd/redigo to newest branch github.com/gomodul… [#3100](https://github.com/beego/beego/pull/3100)
19. ExecElem.FieldByName as local variable [#3039](https://github.com/beego/beego/pull/3039)
20. Allow log prefix [#3145](https://github.com/beego/beego/pull/3145)
21. Refactor yaml config for support multilevel [#3127](https://github.com/beego/beego/pull/3127)
22. Create redis_cluster.go [#3175](https://github.com/beego/beego/pull/3175)
23. Add field comment on create table [#3190](https://github.com/beego/beego/pull/3190)
24. Update: use PathEscape replace QueryEscape [#3200](https://github.com/beego/beego/pull/3200)
25. Update gofmt [#3206](https://github.com/beego/beego/pull/3206)
26. Update: Htmlquote Htmlunquote [#3202](https://github.com/beego/beego/pull/3202)
27. Add 'FOR UPDATE' support for querySet [#3208](https://github.com/beego/beego/pull/3208)
28. Debug stringsToJSON [#3171](https://github.com/beego/beego/pull/3171)
29. Fix defaut value bug, and add config for maxfiles [#3185](https://github.com/beego/beego/pull/3185)
30. Fix: correct MaxIdleConnsPerHost value to net/http default 100. [#3230](https://github.com/beego/beego/pull/3230)
31. Fix: When multiply comment routers on one func [#3217](https://github.com/beego/beego/pull/3217)
32. Send ErrNoRows if the query returns zero rows ... in method orm_query… [#3247](https://github.com/beego/beego/pull/3247)
33. Fix typo [#3245](https://github.com/beego/beego/pull/3245)
34. Add session redis IdleTimeout config [#3239](https://github.com/beego/beego/pull/3239)
35. Fix the wrong status code in prod [#3226](https://github.com/beego/beego/pull/3226)
36. Add method to set the data depending on the accepted [#3182](https://github.com/beego/beego/pull/3182)
37. Fix Unexpected EOF bug in staticfile [#3152](https://github.com/beego/beego/pull/3152)
38. Add code style for logs README [#3146](https://github.com/beego/beego/pull/3146)
39. Fix response http code [#3142](https://github.com/beego/beego/pull/3142)
40. Improve access log [#3141](https://github.com/beego/beego/pull/3141)
41. Auto create log dir [#3105](https://github.com/beego/beego/pull/3105)
42. Html escape before display path, avoid xss [#3022](https://github.com/beego/beego/pull/3022)
43. Acquire lock when access config data [#3250](https://github.com/beego/beego/pull/3250)
44. Fix orm fields SetRaw function error judge problem [#2985](https://github.com/beego/beego/pull/2985)
45. Fix template rendering with automatic mapped parameters (see #2979) [#2981](https://github.com/beego/beego/pull/2981)
46. Fix the model can not be registered correctly on Ubuntu 32bit [#2997](https://github.com/beego/beego/pull/2997)
47. Feature/yaml [#3181](https://github.com/beego/beego/pull/3181)
48. Feature/autocert [#3249](https://github.com/beego/beego/pull/3249)

# beego 1.9.0
1. Fix the new repo address for casbin [#2654](https://github.com/beego/beego/pull/2654)
2. Fix cache/memory fatal error: concurrent map iteration and map write [#2726](https://github.com/beego/beego/pull/2726)
3. AddAPPStartHook func modify [#2724](https://github.com/beego/beego/pull/2724)
4. Fix panic: sync: negative WaitGroup counter [#2717](https://github.com/beego/beego/pull/2717)
5. incorrect error rendering (wrong status) [#2712](https://github.com/beego/beego/pull/2712)
6. validation: support int64 int32 int16 and int8 type [#2728](https://github.com/beego/beego/pull/2728)
7. validation: support required option for some struct tag valids [#2741](https://github.com/beego/beego/pull/2741)
8. Fix big form parse issue [#2725](https://github.com/beego/beego/pull/2725)
9. File log add RotatePerm [#2683](https://github.com/beego/beego/pull/2683)
10. Fix Oracle placehold [#2749](https://github.com/beego/beego/pull/2749)
11. Supported gzip for req.Header has Content-Encoding: gzip [#2754](https://github.com/beego/beego/pull/2754)
12. Add new Database Migrations [#2744](https://github.com/beego/beego/pull/2744)
13. Beego auto generate sort ControllerComments [#2766](https://github.com/beego/beego/pull/2766)
14. added statusCode and pattern to FilterMonitorFunc [#2692](https://github.com/beego/beego/pull/2692)
15. fix the bugs in the "ParseBool" function in the file of config.go [#2740](https://github.com/beego/beego/pull/2740)

## bee 1.9.0 
1. Added MySQL year data type [#443](https://github.com/beego/beego/pull/443)
2. support multiple http methods [#445](https://github.com/beego/beego/pull/445)
3. The DDL migration can now be generated by adding a -ddl and a proper "alter" or "create" as argument value. [#455](https://github.com/beego/beego/pull/455)
4. Fix: docs generator skips everything containing 'vendor' [#454](https://github.com/beego/beego/pull/454)
5. get these tables information in custom the option [#441](https://github.com/beego/beego/pull/441)
6. read ref(pk) [#444](https://github.com/beego/beego/pull/444)
7. Add command bee server to server static folder. 

# beego 1.7.1
新增功能:
1. access log 增加 IP [#2156](https://github.com/beego/beego/pull/2156)
2. orm 增加新接口 ReadForUpdate [#2158](https://github.com/beego/beego/pull/2158)
3. 参数 bind 支持数组 form，columns[0].Data=foo&columns[1].Data=bar&columns[2].Data=baz [#2111](https://github.com/beego/beego/pull/2111)
4. 自定义 recover 函数，增加配置 `beego.BConfig.RecoverFunc`，默认和原来保持一致，但是用户可以自己定义 [#2004](https://github.com/beego/beego/issues/2004)
5. memcache cache 同时支持 byte 和 string 的存储，这样就可以通过 gob 保存 struct [#1521](https://github.com/beego/beego/issues/1521)
6. ORM delete 支持按照指定条件删除 [#1802](https://github.com/beego/beego/issues/1802)
7. swagger 的支持输出 yaml [#2162](https://github.com/beego/beego/pull/2162)
8. 增加 RunController 和 RunMethod,让用户自定义路由规则 [#2017](https://github.com/beego/beego/issues/2017)

修复 bug:
1. 静态目录如果已经存在 index.html,当访问目录的时候不会自动添加 /, 例如访问 /swagger 不会跳转到 /swagger/，这样会导致相对的 css 和 js 访问不存在 [#2142](https://github.com/beego/beego/issues/2142)
2. beego admin ui 里面访问时间排序没有按照 us, ms 排序，而是按照字符排序 [#1877](https://github.com/beego/beego/issues/1877)
3. captcha 生产图片的时候，自定义 height 和 width crash [#2161](https://github.com/beego/beego/issues/2161)
4. DELETE 请求下开启了 CopyBody 情况下，如果 body 为空 panic [#1656](https://github.com/beego/beego/issues/1656)


# beego 1.7.0
新增改进功能：
1. Filter 访问速度提升 7.5 倍以上 [#1799](https://github.com/beego/beego/pull/1799)
2. Gzip 压缩的时候支持不同的 level [#1808](https://github.com/beego/beego/pull/1808)
3. ORM PK 支持负数 [#1810](https://github.com/beego/beego/pull/1810)
4. ORM 支持自定义自增 ID 的值 [#1826](https://github.com/beego/beego/pull/1826)
5. Context 下载文件函数改进：下载文件之前先检查是否存在 [#1827](https://github.com/beego/beego/pull/1827)
6. log增加 `GetLogger` 函数，可以增加相应的前缀 [#1832](https://github.com/beego/beego/pull/1832)

```
package main

import "github.com/astaxie/beego/logs"

func main() {
    logs.Warn("this is a warn message")

    l := logs.GetLogger("HTTP")
    l.Println("this is a message of http")

    logs.GetLogger("orm").Println("this is a message of orm")

    logs.Debug("my book is bought in the year of ", 2016)
    logs.Info("this %s cat is %v years old", "yellow", 3)
    logs.Error(1024, "is a very", "good", 2.5, map[string]int{"id": 1})
    logs.Critical("oh my god")
}
```
![](https://cloud.githubusercontent.com/assets/707691/14017109/f608b658-f1ff-11e5-8d57-72030cfe4f5d.png)
7. session 增加 Log，一旦错误发生可以记录日志. [#1833](https://github.com/beego/beego/pull/1833)
8. logs 包添加两个 public 函数,`EnableFuncCallDepth` 和 `SetLogFuncCallDepth`, 用来设置函数的调用层级. [#1837](https://github.com/beego/beego/pull/1837)
9. 支持 `go run` 运行 beego 的项目代码 [#1840](https://github.com/beego/beego/pull/1840)
10. 添加 `ExecuteTemplate` 函数，这样用户就可以通过这种方式访问 template，而不是直接访问 map，因为 map 有并发读写问题 [#1848](https://github.com/beego/beego/pull/1848)
11. ORM 字段支持 `time` 类型 [#1856](https://github.com/beego/beego/pull/1856)
12. ORM One 接口只获取一条 [#1874](https://github.com/beego/beego/pull/1874)
13. ORM 支持 json jsonb 类型   [#1875](https://github.com/beego/beego/pull/1875)
14. ORM 默认使用 text 类型 [#1879](https://github.com/beego/beego/pull/1879)
15. session 配置三个配置，`EnableSidInHttpHeader` `EnableSidInUrlQuery` `SessionNameInHttpHeader`,
    允许用户可以在 http 头和 URL 中带 sid [#1897](https://github.com/beego/beego/pull/1897)
16. 自动化路由改进生成的文件名，之前太长了 [#1924](https://github.com/beego/beego/pull/1924)
17. 支持复杂的模板引擎. ace jade [#1940](https://github.com/beego/beego/pull/1940)
```
beego.AddTemplateEngine("ace", func(root, path string, funcs template.FuncMap) (*template.Template, error) {
        aceOptions := &ace.Options{DynamicReload: true, FuncMap: funcs}
        aceBasePath := filepath.Join(root, "base/base")
        aceInnerPath := filepath.Join(root, strings.TrimSuffix(path, ".ace"))

        tpl, err := ace.Load(aceBasePath, aceInnerPath, aceOptions)
        if err != nil {
            return nil, fmt.Errorf("error loading ace template: %v", err)
        }

        return tpl, nil
    })
```
[#1940](https://github.com/beego/beego/pull/1940)
18. session 引擎支持 ssdb [#1953](https://github.com/beego/beego/pull/1953)
19. RenderForm 支持输出 required [#1993](https://github.com/beego/beego/pull/1993)
20. 让打印的 beego 日志更加美观 [#1997](https://github.com/beego/beego/pull/1997)
![](https://cloud.githubusercontent.com/assets/1248967/16153054/f654b08e-34a4-11e6-894d-24f16ab847a7.png)
21. ORM 支持 struct 中带有 `time.Time` 指针 [#2006](https://github.com/beego/beego/pull/2006)
22. Controller 中增加 `TplPrefix` 这样就可以在 baseController 制定读取模板的前缀目录 [#2030](https://github.com/beego/beego/pull/2030)
23. jsonb 函数中增加 js 函数的判断，避免函数不存在时候出错.  [#2045](https://github.com/beego/beego/pull/2045)
24. ORM 增加 `InsertOrUpdate` 函数 [#2053](https://github.com/beego/beego/pull/2053)
25. Filter 函数增加重置参数的参数. 因为 `beego.InsertFilter("*", beego.BeforeStatic, RedirectHTTP)`
的时候，参数会赋值给 `:splat`,从而影响后续如果路由里面也有想用的路由，
那么就会引起冲突，因此增加这样的函数以方便用户重置。 [#2085](https://github.com/beego/beego/pull/2085)
26. session 包配置采用对象初始化，而抛弃传递 json 的方式. 如果独立使用session包的可能会引起兼容性问题 [#2096](https://github.com/beego/beego/pull/2096)
27. Swagger 迁移到2.0版本，现在生产的代码无需依赖 API，直接生产 swagger.json

bugfix:
1. 静态路由中 `/m` 自动跳转到 `/m/` [#1792](https://github.com/beego/beego/pull/1792)
2. test 的时候解析配置文件出错 [#1794](https://github.com/beego/beego/pull/1794)
3. 文件 rotato 的时候产生 race condition [#1803](https://github.com/beego/beego/pull/1803)
4. 修复 multiple response.WriteHeader calls 的错误 [#1805](https://github.com/beego/beego/pull/1805)
5. ORM 如果主键是 uint 的时候 panic [#1828](https://github.com/beego/beego/pull/1828)
6. 日志 rotate 的时候如果当前时间小于 2000 panic [#]()
7. context 重用导致 XSRF 重用[#1863](https://github.com/beego/beego/pull/1863)
8. ORM InsertMulti 的时候当是 * 类型时 panic [#1882](https://github.com/beego/beego/pull/1882)
9. task 中任务在很微小的时间内可能存在执行多次的情况 [#1909](https://github.com/beego/beego/pull/1909)
10. IE 浏览器下载文件名混乱 [#1912](https://github.com/beego/beego/pull/1912)
11. ORM DISTINCT 实现 [#1938](https://github.com/beego/beego/pull/1938)
12. Logs 包里面设置文件的 permit 时候，int 无法设置. [#1948](https://github.com/beego/beego/pull/1948) [#2003](https://github.com/beego/beego/pull/2003)
13. QueryRow 和 QueryRows 查询获取数据后外键字段不填充值 [#1964](https://github.com/beego/beego/pull/1964)
14. 当 beego 应用跑在代理之后的时候，scheme 通过 `X-Forwarded-Proto` 获取 [#2050](https://github.com/beego/beego/pull/2050)
15. 静态文件访问目录时候跳转到 `目录/` 的时候自动带上参数 [#2064](https://github.com/beego/beego/pull/2064)

# beego 1.6.1
新增功能：
1. ORM 支持 Oracle 驱动
2. ORM 的 Model 支持 inline
3. Cache 支持 ssdb引擎
4. console 支持颜色输出配置
5. 添加 travis 的自动化集成测试
6. 日志新增 mulitfile 引擎，支持不同级别的输出到不同的文件

bugfix：
1. cookie 时间设置
2. 路由规则里面的匹配 [#1580](https://github.com/beego/beego/issues/1580)
3. 在 beego.Run() 之前没有 log 输出
4. config 获取 []string 为空的时候返回为空，应该返回 nil
5. ini 接口保存的时候需要注释不正确
6. 异步存储日志的时候时间可能延迟的问题
7. 配置文件解析两次，导致部署 key 获取失败
8. 正则路由无法解析本身带有 `()` 的问题
9. mail发送中文附件和 title 乱码的问题
10. ORM 里面缺少 Distinct 的接口定义
11. Layout 编译失败
12. logrotate 的时候文件名不正确
13. CORS 插件失败的时候不生效
14. filters 的路径参数和路由参数冲突
15. 静态文件找不到返回 200，应该返回 404
16. 添加 GroupBy 的 interface 支持
17. Go1.6 的并发访问 map 引起静态文件换成崩溃
18. httplib JSONBody 输出的时候采用 json.Encoder 会输出一个额外的换行符
19. 异步模式下，log 调用 flush，Close 的时候日志丢失

# beego 1.6.0
新功能：

1. 文件 log 支持 rotate 支持类似 `xx.2013-01-01.2.log` 这样的输出 [#1265](https://github.com/beego/beego/pull/1265)
2. context.response 支持了原生的 Flush，Hijack，CloseNotify
3. ORM 支持 Distinct 操作 [#1276](https://github.com/beego/beego/pull/1276)
4. 新增加模板函数 map_get [#1305](https://github.com/beego/beego/pull/1305)
5. ORM 支持 tidb 引擎 [#1366](https://github.com/beego/beego/pull/1366)
6. httplib 请求参数支持 []string [#1308](https://github.com/beego/beego/pull/1308)
7. ORM querySeter 添加 GroupBy 方法 [#1345](https://github.com/beego/beego/pull/1345)
8. Session 的 MySQL 引擎支持自定义表名 [#1348](https://github.com/beego/beego/pull/1348)
9. log 的 file 引擎性能提升 30%，同时支持自定义创建的文件权限 [#1560](https://github.com/beego/beego/pull/1560)
10. session 支持通过 query 获取 [#1507](https://github.com/beego/beego/pull/1507)
11. Cache 模块支持多个 Cache 对象，之前调用 NewCache 获取的是同一个 Cache，现在会初始化不同的 Cache 对象。
12. validation 支持自定义验证函数

bugfix:

1. context 里面 bind 函数如果参数为空 crash [#1245](https://github.com/beego/beego/issues/1245)
2. ORM 中 manytomany 获取 reverse 的时候出错。[#671](https://github.com/beego/beego/issues/671)
3. http: multiple response.WriteHeader calls [#1329](https://github.com/beego/beego/pull/1329)
4. ParseForm 解析日期使用当前的 timezone [#1343](https://github.com/beego/beego/pull/1343)
5. log 引擎里面 Smtp 发送邮件无法认证
6. 修复路由规则的一些 issue: `/topic/:id/?:auth`, `/topic/:id/?:auth:int` [#1349](https://github.com/beego/beego/pull/1349)
7. 修复注释文档解析的时候 nil 引起 crash [#1367](https://github.com/beego/beego/pull/1367)
8. static 目录下的 index.html 无法读取[#1508](https://github.com/beego/beego/pull/1508)
9. dbBase.Update 失败不返回 err [#1384](https://github.com/beego/beego/pull/1384)
10. validation 里面设置的 Required 只对 int 有效，int64 无效
11. ORM 创建外键是 string 类型的主键时创建 varchar(0) 的字符问题 [#1379](https://github.com/beego/beego/pull/1379)
12. graceful 同时开启 http 和 https 的时候出错 [#1414](https://github.com/beego/beego/pull/1414)
13. ListenTCP4 开启之后如果 httpaddr 为空还是监控 TCP6
14. migration 不支持 postgres [#1434](https://github.com/beego/beego/pull/1434)
15. ORM text、bool 等默认值问题导致创建表出错
16. graceful 导致 panic 问题 negative WaitGroup counter

优化:

1. example 移到了 [samples](https://github.com/beego/samples)
2. 所有代码符合 golint 规范
3. 重写路由树底层，性能提升三倍左右
4. 每次请求的 context 采用 sync.Pool 复用，内存和性能提升
5. 模板编译优化速度，按需编译 [#1298](https://github.com/beego/beego/pull/1298)
6. 优化了 beego 的配置管理，采用统一的 BConfig，更易读易管理
7. 优化了 beego 的整体结构代码，使得代码更易读维护
8. 所有初始化的信息统一到 AddAPPStartHook 函数中去，易于管理
9. 移除了 middleware，之后全部采用 plugins 来管理插件
10. 重构 Error 处理，使得 Error 更加易懂

# beego 1.5.0
新功能:

1. 优雅重启模块：grace
2. httplib 增加 JsonBody 函数，支持 raw body 以 Json 格式发送
3. context input 增加 AcceptsHtml AcceptsXml AcceptsJson 函数
4. 配置文件优先从 Runmode 中获取
5. httplib 支持 gzip
6. Log 模块默认不采用异步方式
7. validation 增加循环嵌套验证
8. 增加 apk mime
9. ORM 支持 eq 和 ne

bugfix:

1. ledis 驱动的参数错误
2. 当页面放置一段时间，验证码将从缓存中失效。当用户再来刷新验证码将出现验证码 404。对于 reload 操作应该直接生成验证码。
3. Controller 定义 Error 异常
4. 修复 cookie 无法在 window 下的 IE 正常工作
5. GetInt 函数当获取不存在的变量是返回 nil 错误
6. 增加更多的手机验证码方式
7. 修复路由的匹配问题
8. panic 返回 http 200
9. redis session 引起数据库设置错误
10. https 和 http 直接的 session 无法共享
11. memcache session 引擎当没有数据的时候返回错误

# beego 1.4.3
新功能:

1. ORM 数据库创建和修改的时候支持 default 设置
2. 改进日志文件行数统计
3. session ledis 支持选择数据库
4. session redis 支持选择数据库
5. cache redis 支持选择数据库
6. UrlFor 支持任意类型的参数
7. controller 中 GetInt/GetString 等 Get 系列函数支持默认值, 例如：GetInt("a",12)
8. 增加 CompareNot/NotNil 模板函数
9. 支持 Controller 定义错误处理，更多请参考 [controller Error](http://beego.vip/docs/mvc/controller/errors.md#controller%E5%AE%9A%E4%B9%89error)
10. ParseForm 增加支持 slices
11. 改进 ORM interface，可以模拟 interface

bugfix:

1. context subdomain 获取的子域名不正确
2. beego.AppConfig.Strings 当数据为空时判定不正确
3. utils/pagination 修复不能修改分页属性
4. 路由处理中如果请求的 URL 是空导致 crash 的问题
5. adminui 中 task 点击无法执行
6. CGI 模式退出进程后 Socket 文件没有删除


# beego 1.4.2
新功能：

1. 增加了 SQL 构造器，参考了 ZEND 框架的 ORM
2. Controller 获取参数增加了 GetInt(), GetInt8(), GetInt16(), GetInt32(), GetInt64()
3. 优化日志提示，增加日志输出过滤设置 FilterHandler，默认静态文件不输出匹配日志
4. 静态目录支持 index.html 输出，静态目录自动增加 /
5. flash 支持 success 和 set 函数，支持各种一次性的数据
6. 路由支持大小写忽略设置，RouterCaseSensitive，默认是大小写敏感的 URL，根据用户注册的URL进行匹配
7. 配置文件支持自定义的变量获取，beego.AppConfig.String("myvar") 在 dev 模式下返回456，在其他模式下返回 123

    > runmode = dev
    > myvar = 123
    > [dev]
    > myvar = 456

8. ini 配置文件支持 include 语法，在配置文件中允许 include 其他配置文件：

    > appname = btest
    > include b.conf

9. utils 下增加分页组件，可以方便用户编写分页相关的应用。
10. 增加 BEEGO_RUNMODE 环境变量，用户在部署的时候只要通过改变量方便切换应用的不同模式
11. toolbox 增加获取 statistic 的 Json 函数
12. utils 下的 mail 发送内嵌附件发送
13. 允许用户通过标准 IO 开启 fastcgi
14. redis Session 引擎，采用 SETEX 命令兼容老版本的 redis
15. RenderForm 支持 html id 和 class，使用 id 和 class tag
16. ini 配置文件支持 BOM 头
17. Session 增加新的引擎 ledis
18. 改进 httplib 文件上传，采用了 io.Pipe 支持超大文件上传
19. 支持应用启动直接绑定到 TCP4 地址上，Go 默认是绑定到 ipv6，增加配置参数 ListenTCP4
20. 表单数据渲染支持 off/on/yes/no/1/0 解析到 bool，支持 time 格式的解析
21. 简化了 SessionID 的生成，不再采用 hmac_sha1 算法，直接通过 golang 内置的 rand 获取

bugfix:

1. 模拟 PUT 和 DELETE 时，_method 的值没有大写，导致 XSRF 验证失败
2. cache 如果在 StartAndGC 初始化失败时，没有返回错误信息
3. httplib 修复 User-Agent 设置不起作用
4. DelStaticPath 优化/处理
5. 静态目录多个的时候，文件只会在第一个静态目录找
6. Filter 函数在 AfterExec 和 FinishRouter 之后多个 Filter 不能执行的问题
7. 修复在请求方法是模拟的 _method 是 PUT 或者 DELETE 的时候无法正确路由
8. 修复了 mime 没有初始化的问题
9. log 输出文件以及行号不正确
10. httplib 修复了当只有一个文件上传一个参数是不能发送的问题
11. 改进了 Abort 的输出信息，之前如果是没有定义的错误信息不会输出
12. 修复 namespace 循环嵌套中，如果外层没有 Filter 的情况下内层 Filter 无法添加的问题
13. 路由包含多层参数时，路由匹配出错 #824
14. 注释路由，如果存在多个 namespace 的时候，一个更新，另一个信息丢失 #770
15. urlfor函数调用多余 {{placeholder}} 问题 #759

# beego 1.4.1
主要更新：

1. context.Input.Url 获取 path 信息，去除了域名，scheme 等信息
2. 增加插件 apiauth，模拟 AWS 的加密请求
3. 精简 debug 输出的路由信息
4. orm 字段支持指针类型
5. 改进了 httplib 功能，增加了 BasicAuth，多次请求缓存等功能

bugfix:
1. _method 模拟请求 put 和 delete，参数大小写不统一
2. 路由 *.* 和其他路由正则混用情况下无法解析

# beego 1.4.0
这个版本整整憋了两个月时间，主要是我们真的做了好多功能性上面的改进，这里要感谢所有给 beego 贡献的用户，也感谢给 beego 持续提各种改进意见的用户，下面是我们这次改进的特性

1. bee 工具的完整性改进，bee 现在支持了如下功能：

	bee api 直接从数据库读取数据库表，一键生成 API 应用带文档，详细介绍看视频：http://www.tudou.com/programs/view/aM7iKLlBlrU/
	- bee generate 命令，这个是新增加的命令，可以用来自动化生成代码，主要有如下子命令：

	     - scaffold 类似其他框架的脚手架功能，生成 controller、model、view、migration

	     - model 生成 CRUD 的 model

	     - controller 生成 CRUD 的 controller

	     - view 生成 CRUD 的 view 文件，内容为空，需要用户自己做 UI 界面

	     - migration 生成 migration 文件

	     - appcode 从数据库根据表结构生成 model、controller、router

	     - docs 从 controller 注释自动化生成 swagger 文档
	- bee migrate 命令，执行 migration，支持如下子命令

	     - migrate 执行所有新的 migration

	     - rollback 回滚最后一次执行的 migration

	     - reset 回滚所有的 migration

	     - refresh 回滚所有的 migration 并从头执行全部的 migration
	- bee run改进，默认支持了 watchall 功能，增加了两个参数 gendoc 和 downdoc

2. config 模块增加新的接口，现在 config 模块支持如下接口，支持直接保存文件：

	```
	type ConfigContainer interface {
	    Set(key, val string) error   // support section::key type in given key when using ini type.
	    String(key string) string    // support section::key type in key string when using ini and json type; Int,Int64,Bool,Float,DIY are same.
	    Strings(key string) []string //get string slice
	    Int(key string) (int, error)
	    Int64(key string) (int64, error)
	    Bool(key string) (bool, error)
	    Float(key string) (float64, error)
	    DefaultString(key string, defaultval string) string      // support section::key type in key string when using ini and json type; Int,Int64,Bool,Float,DIY are same.
	    DefaultStrings(key string, defaultval []string) []string //get string slice
	    DefaultInt(key string, defaultval int) int
	    DefaultInt64(key string, defaultval int64) int64
	    DefaultBool(key string, defaultval bool) bool
	    DefaultFloat(key string, defaultval float64) float64
	    DIY(key string) (interface{}, error)
	    GetSection(section string) (map[string]string, error)
	    SaveConfigFile(filename string) error
	}
	```

3. middleware中支持另一种 i18n 的支持：

	```
	I18N = middleware.NewLocale("conf/i18n.conf", beego.AppConfig.String("language"))
	```

	配置文件如下：

	```
	{
	  "E-mail Address": {
	    "en": "E-mail Address",
	    "zh": "邮箱地址",
	    "vn": "อีเมล"
	  },
	  "Username": {
	    "en": "Ussername",
	    "zh": "用户名",
	    "vn": "t&ecirc;n truy nhập"
	  }
	}
	```

	使用如下：

	`I18N.Translate("username", "vn")`

4. namespace前缀支持正则：

	```
	beego.NewNamespace("/v1/:uid",
	    beego.NSNamespace("/customer",
	        beego.NSInclude(
	            &controllers.CustomerController{},
	            &controllers.CustomerCookieCheckerController{},
	        ),
	    ),
	)
	```

5. cache 和 session 模块的 memcache、redis 引擎修改到最新版本的驱动

6. 增加开发打印路由调试功能:

	```
	2014/08/22 09:55:40 [I] | GET | /          | 7.660221504s     | match      | / |
	2014/08/22 09:55:40 [I] | GET | /          | 13.421869836s    | match      | / |
	2014/08/22 09:55:40 [I] | GET | /          | 1.726185752s     | match      | / |
	2014/08/22 09:55:40 [I] | GET | /user/login| 7.494079ms       | match      | /user/login |
	```

7. log 的等级符合 RFC5424 规范

8. 静态文件处理支持 robots.txt，用户放在 static 目录下即可

9. 增加和简化 plugins 功能：

	auth 支持 basicauth，详细使用请看 https://godoc.org/github.com/beego/beego/plugins/auth
	cors 支持跨站调用，详细使用请看 https://godoc.org/github.com/beego/beego/plugins/cors

10. 新增了 AdminUI，用户在 EnableAdmin 的情况下，可以通过界面简单地获取当前应用的各种状态，同时可以很容易的调试性能，监控系统，执行任务，获取配置等

	![](../images/adminui.png)

11. session 配置现在支持设置 cookie domain

12. 新增 migration 包，支持 migration 的功能

13. getconfg 方法改为 public 方法，用户就可以通过改方法获取相应 runmode 下的配置文件

14. 改进 httplib 的方法支持 SetAgent 和 BasicAuth 的请求，httplib 支持请求一次，读取多次

修复 bug：

1. file session 在部分情况下内容消失问题
2. docs 自动化生成，文件不更新
3. 路由 namespace 的前缀不支持
4. orm 修正 detect engine
5. 修复 captcha 里面当用户验证码输入长度不对时不进行更新
6. 调用 setstatus 之后后面调用的 setHeader 全部无效的问题
7. 修复 smtp 发送邮件需要验证的情况
8. 修复 utils 下 safemap 的 items 问题
9. 修复 geturl 函数当参数多个时不带?的问题

# beego 1.3.0
经过了一个多月的开发，我们很高兴的宣布，beego 1.3.0来了，这个版本我们做了非常多好玩并且有用的功能，升级请看[升级指南](http://beego.vip/docs/intro/upgrade.md)

## 路由重写
这一次路由进行了全部改造，从之前的三个路由模式，改成了 tree 路由，第一性能得到了提升，第二路由支持的格式更加丰富，第三路由更加符合我们的思考方式，

例如现在注册如下路由规则：

	/user/astaxie
	/user/:username

如果你的访问地址是 `/user/astaxie`，那么优先匹配固定的路由，也就是第一条，如果访问是 `/user/slene`，那么就匹配第二个，和你注册的路由的先后顺序无关

## namespace 更优雅
设计 namespace 主要是为了大家模块化设计的，之前是采用了类似 jQuery 的链式方式，当然新版本也是支持的，但是由于 gofmt 的格式无法很直观的看出来整个路由的目录结构，所以我采用了多参数注册方式，现在看上去就更加的优雅：

```
ns :=
beego.NewNamespace("/v1",
    beego.NSNamespace("/shop",
        beego.NSGet("/:id", func(ctx *context.Context) {
            ctx.Output.Body([]byte("shopinfo"))
        }),
    ),
    beego.NSNamespace("/order",
        beego.NSGet("/:id", func(ctx *context.Context) {
            ctx.Output.Body([]byte("orderinfo"))
        }),
    ),
    beego.NSNamespace("/crm",
        beego.NSGet("/:id", func(ctx *context.Context) {
            ctx.Output.Body([]byte("crminfo"))
        }),
    ),
)
```
更多详细信息请参考文档：[namespace](http://beego.vip/docs/mvc/controller/router.md#namespace)

## 注解路由
```
// CMS API
type CMSController struct {
    beego.Controller
}

func (c *CMSController) URLMapping() {
    c.Mapping("StaticBlock", c.StaticBlock)
    c.Mapping("AllBlock", c.AllBlock)
}

// @router /staticblock/:key [get]
func (this *CMSController) StaticBlock() {

}

// @router /all/:key [get]
func (this *CMSController) AllBlock() {
}
```
更多请参考文档：[注解路由](http://beego.vip/docs/mvc/controller/router.md#%E6%B3%A8%E8%A7%A3%E8%B7%AF%E7%94%B1)

## 自动化文档
自动化文档一直是我梦想中的一个功能，这次借着公司的项目终于实现了出来，我说过 beego 不仅仅要让开发 API 快，而且让使用 API 的用户也能快速的使用我们开发的 API，这个就是我开发这个项目的初衷。

可以通过注释自动化的生成文档，并且在线测试，详细的请看下面的截图

![](../images/docs.png)

而且可以通过文档进行 API 的测试：

![](../images/doc_test.png)

更多请参考文档：[自动化文档](http://beego.vip/docs/advantage/docs.md)
## config 支持不同模式的配置
在配置文件里面支持 section，可以有不同的 Runmode 的配置，默认优先读取 runmode 下的配置信息，例如下面的配置文件：

	appname = beepkg
	httpaddr = "127.0.0.1"
	httpport = 9090
	runmode ="dev"
	autorender = false
	autorecover = false
	viewspath = "myview"

	[dev]
	httpport = 8080
	[prod]
	httpport = 8088
	[test]
	httpport = 8888

上面的配置文件就是在不同的 runmode 下解析不同的配置，例如在 dev 模式下，httpport 是 8080，在 prod 模式下是 8088，在 test 模式下是 8888。其他配置文件同理。解析的时候优先解析 runmode 模式的配置，然后解析默认的配置。

## 支持双向的 SSL 认证
```
config := tls.Config{
    ClientAuth: tls.RequireAndVerifyClientCert,
    Certificates: []tls.Certificate{cert},
    ClientCAs: pool,
}
config.Rand = rand.Reader

beego.BeeApp.Server.TLSConfig = &config
```
## beego.Run支持带参数

beego.Run() 默认执行HttpPort

beego.Run(":8089")

beego.Run("127.0.0.1:8089")

## XSRFKEY 的 token 从 15 个字符增加到 32 个字符，增强安全性

## 删除热更新

## 模板函数增加 Config，可以方便的在模板中获取配置信息

	{{config returnType key defaultValue}}

	{{config "int" "httpport" 8080}}

## httplib 支持 cookiejar 功能，感谢 curvesft

## orm 时间格式，如果为空就设置为 nil，感谢 JessonChan

## config 模块支持 json 解析就一个 array 格式，感谢 chrisport

## bug fix
- 静态文件目录循环跳转
- fix typo


# beego 1.2.0
大家好,经过我们一个多月的努力,今天我们发布一个很帅的版本,之前性能测试框架出来 beego 已经跃居 Go 框架第一了,虽然这不是我们的目标,我们的目标是做最好用,最易用的框架. http://www.techempower.com/benchmarks/#section=data-r9&hw=i7&test=json 但是这个版本我们还是在性能和易用性上面做了很多改进.应该说性能更加的接近 Go 原生应用.

### 新特性:

#### 1. namespace 支持

```
	beego.NewNamespace("/v1").
		Filter("before", auth).
		Get("/notallowed", func(ctx *context.Context) {
		ctx.Output.Body([]byte("notAllowed"))
	}).
		Router("/version", &AdminController{}, "get:ShowAPIVersion").
		Router("/changepassword", &UserController{}).
		Namespace(
		beego.NewNamespace("/shop").
			Filter("before", sentry).
			Get("/:id", func(ctx *context.Context) {
			ctx.Output.Body([]byte("notAllowed"))
		}))
```

上面这个代码支持了如下这样的请求URL
- GET       /v1/notallowed
- GET       /v1/version
- GET       /v1/changepassword
- POST     /v1/changepassword
- GET       /v1/shop/123

而且还支持前置过滤,条件判断,无限嵌套 namespace

#### 2. beego 支持更加自由化的路由方式

RESTful的自定义函数

- beego.Get(router, beego.FilterFunc)
- beego.Post(router, beego.FilterFunc)
- beego.Put(router, beego.FilterFunc)
- beego.Head(router, beego.FilterFunc)
- beego.Options(router, beego.FilterFunc)
- beego.Delete(router, beego.FilterFunc)

```
beego.Get("/user", func(ctx *context.Context) {
	ctx.Output.Body([]byte("Get userlist"))
})
```
更加自由度的 Handler

- beego.Handler(router, http.Handler)

可以很容易的集成其他服务

```
import (
    "http"
    "github.com/gorilla/rpc"
    "github.com/gorilla/rpc/json"
)

func init() {
    s := rpc.NewServer()
    s.RegisterCodec(json.NewCodec(), "application/json")
    s.RegisterService(new(HelloService), "")
    beego.Handler("/rpc", s)
}
```

#### 3. 支持从用户请求中直接数据 bind 到指定的对象

例如请求地址如下

	?id=123&isok=true&ft=1.2&ol[0]=1&ol[1]=2&ul[]=str&ul[]=array&user.Name=astaxie

```
var id int
ctx.Input.Bind(&id, "id")  //id ==123

var isok bool
ctx.Input.Bind(&isok, "isok")  //isok ==true

var ft float64
ctx.Input.Bind(&ft, "ft")  //ft ==1.2

ol := make([]int, 0, 2)
ctx.Input.Bind(&ol, "ol")  //ol ==[1 2]

ul := make([]string, 0, 2)
ctx.Input.Bind(&ul, "ul")  //ul ==[str array]

user struct{Name}
ctx.Input.Bind(&user, "user")  //user =={Name:"astaxie"}
```

#### 4. 优化解析 form 的流程,让性能更加提升

#### 5. 增加更多地 testcase 进行自动化测试

#### 6. admin 管理模块所有的增加可点击的链接,方便直接查询

#### 7. session 的除了 memory 之外的引擎支持 struct 存储

#### 8. httplib 支持文件直接上传接口

```
b:=httplib.Post("http://beego.vip/")
b.Param("username","astaxie")
b.Param("password","123456")
b.PostFile("uploadfile1", "httplib.pdf")
b.PostFile("uploadfile2", "httplib.txt")
str, err := b.String()
if err != nil {
    t.Fatal(err)
}
```
httplib 支持自定义协议版本

#### 9. ORM 支持 struct 中有 unexport 的字段

#### 10. XSRF 支持 controller 级别控制是否启用, 之前 XSRF 是全局设置只要开启了就会影响所有的 POST PUT DELET 请求,但是项目中可能 API 和页面共存的情况,页面可能不需要类似的 XSRF,因此支持在 Prepare 函数中设置值来控制 controller 是否启用 XSRF. 默认是 true,也就是根据全局的来执行.用户可以在 prepare 中设置是否关闭.

```
func (a *AdminController) Prepare(){
       a.EnableXSRF = false
}
```

#### 11. controller 支持 ServeFormatted 函数,支持根据请求 Accept 来判断是调用 ServeJson 还是 ServeXML

#### 12. session 提供 memcache 引擎

#### 13. Context 中的 Download 函数支持自定义文件名提供下载

## bug 修复

1. session 的 Cookie 引擎修复无法设置过期的 bug
2. 修复 flash 数据的存储和解析问题
3. 修复所有 go vet 出现的问题
4. 修复 ParseFormOrMulitForm 问题
5. 修复只有 POST 才能解析 raw body,现在支持除了 GET 和 HEAD 之外的其他请求
6. config 模块修复 xml 和 yaml 无法解析的问题

# beego 1.1.4

发布一个紧急的版本, beego 存在一个严重的安全漏洞,请大家更新到最新版本. 顺便把最近做的一起发布了

1. 紧急修复一个安全漏洞,稍后会在 beego/SECURITY.md 公布详细的情况

2. 静态文件处理独立到文件

3. 第三方依赖库移除,目前如果你使用 session/cache/config,使用的是依赖第三方库的,那么现在都移到了子目录,如果你想使用这些就需要在使用的地方采用 mysql 类似的方式引入

	```
	import (
	     "github.com/beego/beego/v2"
	   _ "github.com/beego/beego/v2/session/mysql"
	)
	```
4. 修改部分导出的函数为 private,因为外部不需要调用

5. 优化 formparse 的过程,根据不同的 content-type 进行解析

发布时间: 2014-04-08

# beego 1.1.3
这是一个 hotfix 的版本,主要是修复了以下 bug

1. console 日志输出,如果不设置配置文件,不能正常输出

2. 支持了 go run main.go,但是 main.go 没有遵循 beego 的目录结构,自定义了配置文件或者不存在配置文件,就会 panic 找不到 app.conf.

3. 支持了在 go test 中解析配置,但是实际上调用 TestBeegoInit 无法解析配置文件

发布时间: 2014-04-04

# beego 1.1.2
beego 1.1.2 版本发布,这个版本主要是一些改进:

1. 增加 ExceptMethodAppend 函数,支持 autorouter 的时候过滤一些函数

2. 支持自定义 FlashName,FlashSeperator

3. ORM 支持自定义的类型，例如 type MyInt int 这种

4. 修复验证模块返回自定义验证信息

5. 改进 logs 模块, 增加 Init 处理 error,设置一些不必要的 public 函数为 private

6. 增加 PostgreSQL 的 session 引擎

7. logs 模块,支持输出调用的文件名和行号,增加设置函数 EnableFuncCallDepth,默认关闭

8. 修改 session 模块中 Cookie 引擎的一个隐藏 bug

9. 模板解析错误的时候,提示语进行了改进

10. 允许用户通过 Filter 修改 Context,跳过 beego 的路由查找方法,直接使用自己的路由规则.增加参数 RunController 和 RunMethod

11. 支持 go run main.go 执行 beego 的应用

12. 支持 go test 执行测试用例,无法读取配置文件,模板的问题,增加 TestBeegoInit 函数调用.

发布时间: 2014-04-03

# beego 1.1.1
这个版本主要是一些 bug 的修复和增加新功能

1. session 模块 file 引擎无法删除文件,不断刷新引起的文件读取失败问题

2. 文件缓存无法读取 struct,改进 gob 自动化注册

3. session 模块增加新引擎 couchbase

4. httplib 支持设置 transport 和 proxy

5. 改进 context 中 Cookie 函数,默认支持 httponly,以及其他一些默认参数行为

6. 验证模块的改进,支持更多地手机号码

7. getstrings 函数行为也改成 getstring 一样,不需要自己 parseform

8. session 模块 redis 引擎,在连接失败的情况下返回错误

9. 修复无法添加 GroupRouters 的 bug 问题

10. 改进多个静态文件的一些潜在 bug,路径匹配问题,以及自动跳转静态目录显示.

11. ORM 增加 GetDB 获取已连接的 *sql.DB

12. ORM 增加 ResetModelCache 重置已注册缓存的模型 struct，方便写测试

13. ORM 支持 between

14. ORM 支持 sql.Null* 类型

15. 修改 auto_now_add，用户有自定义值时跳过自动设置时间

发布时间: 2014-03-12

# beego 1.1.0
这个版本增加了一些新特性，修复了一些 bug

新特性

1. 支持 AddAPPStartHook 函数
2. 支持插件模式，支持 AddGroupRouter，用于插件路由设置
3. response 支持 HiJacker接口
4. AddFilter 支持批量匹配
5. session 重构，支持 Cookie 引擎
6. 主流 ORM 性能测试
7. config 增加 strings 接口，允许设置
8. 支持 controller 级别的模板渲染控制
9. 增加插件 basicauth，可以方便的使用该插件实现认证
10. #436 一次插入多个对象
11. #384 query map to struct

bugfix

1. 修复 FileCache的bug
2. websocket 的例子修正引用库
3. 当发生程序内部错误时。http 的 status 默认修改为 500 而不是 200
4. gmfim map in memzipfile.go file should use some synchronization mechanism (for example sync.RWMutex) otherwise it errors sometimes.
5.  #440 on_delete 不自动删除的问题
6. #441 时区问题

发布时间: 2014-02-10

# beego 1.0.0
经过了四个多月的重构开发，beego 终于发布了第一个正式稳定版本。这个版本我们进行了重构，同时针对很多细节进行了改进。下面列一些主要的改进功能：

1. 模块化的设计，现在基本上 beego 做成一个轻量的组装框架，重模块的设计，目前实现了cache、config、logs、sessions、httplibs、toolbox、orm、context 等八个模块，以后可能会更多。用户可以直接引用这些模块应用于自己的应用中，不仅仅局限于Web应用，beego 用户中有应用 logs、config、cache 这些模块到页游、手游中。

2. 工程化的设计，部署项目之后，经常需要进行对线上程序进行各种信息的统计和分析，统计包括 QPS，分析包括 GC、内存使用量、CPU，如果出现问题的时候我们还希望通过 profile 来调试，那么 beego 都为你考虑到了这些，集成了监控模块，默认是关闭的，用户可以开启，并在另一个端口监听，通过 http://127.0.0.1:8088/ 访问。

3. 详细的文档，这个版本的文档全部是新写的，在之前文档用户的各方面反馈之后，进行了很多细节上面的改进，目前文档中英文版本都已经完成，中英文文档的评论分离，针对不同的用户群交流。

4. 丰富的示例，这一次更新我们开发组写了三个例子，聊天室、短域名、todo 任务三个比较有典型意义的例子。让用户在熟悉 beego 之前有一个更深入的了解。

5. 全新设计的官方网站，这一次我们通过社区获得了很多人的帮助，logo 设计，网站 UI 的改进。

6. 越来越多的用户，官方网站列举了一些典型的用户，都是一些比较大的公司，他们内部都在使用beego开发对外的 API 应用，说明 beego 是得到了线上项目验证的框架。

7. 越来越活跃的社区，在 github 上面目前已经差不多有 390 个的 issue，贡献者超过 36 个，commit 超过了 700 个，Google groups 目前还在稳步发展中。

8. 周边产品越来越多，基于beego的开源产品也越来越多，例如 cms 系统，https://github.com/insionng/toropress  例如管理后台系统，https://github.com/beego/admin

9. beego 的辅助工具越来越强大，bee 工具是专门辅助用户开发 beego 应用的，可以快速的创建应用，动态编译，打包部署等

发布时间: 2013-12-19
