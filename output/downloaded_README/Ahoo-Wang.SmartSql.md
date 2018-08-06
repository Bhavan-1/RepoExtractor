<p align="center">
  <a href="https://doc.smartsql.net/" target="_blank"><img width="100"src="https://raw.githubusercontent.com/Ahoo-Wang/SmartSql/master/SmartSql.png"></a>
</p>

# 简介

[![Join the chat at https://gitter.im/SmartSql-DotNet/Lobby](https://badges.gitter.im/SmartSql-DotNet/Lobby.svg)](https://gitter.im/SmartSql-DotNet/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

>[SmartSql-Starter](https://github.com/Ahoo-Wang/SmartSql-Starter)

## Nuget Packages

| Package | NuGet Stable |  Downloads |
| ------- | -------- | ------- |
| [SmartSql](https://www.nuget.org/packages/SmartSql/) | [![SmartSql](https://img.shields.io/nuget/v/SmartSql.svg)](https://www.nuget.org/packages/SmartSql/)  | [![SmartSql](https://img.shields.io/nuget/dt/SmartSql.svg)](https://www.nuget.org/packages/SmartSql/) |
| [SmartSql.TypeHandler](https://www.nuget.org/packages/SmartSql.TypeHandler/) | [![SmartSql.TypeHandler](https://img.shields.io/nuget/v/SmartSql.TypeHandler.svg)](https://www.nuget.org/packages/SmartSql.TypeHandler/)  | [![SmartSql.TypeHandler](https://img.shields.io/nuget/dt/SmartSql.TypeHandler.svg)](https://www.nuget.org/packages/SmartSql.TypeHandler/) |
| [SmartSql.DyRepository](https://www.nuget.org/packages/SmartSql.DyRepository/) | [![SmartSql.DyRepository](https://img.shields.io/nuget/v/SmartSql.DyRepository.svg)](https://www.nuget.org/packages/SmartSql.DyRepository/)  | [![SmartSql.DyRepository](https://img.shields.io/nuget/dt/SmartSql.DyRepository.svg)](https://www.nuget.org/packages/SmartSql.DyRepository/) |
| [SmartSql.DIExtension](https://www.nuget.org/packages/SmartSql.DIExtension/) | [![SmartSql.DIExtension](https://img.shields.io/nuget/v/SmartSql.DIExtension.svg)](https://www.nuget.org/packages/SmartSql.DIExtension/)  | [![SmartSql.DIExtension](https://img.shields.io/nuget/dt/SmartSql.DIExtension.svg)](https://www.nuget.org/packages/SmartSql.DIExtension/) |
| [SmartSql.Cache.Redis](https://www.nuget.org/packages/SmartSql.Cache.Redis/) | [![SmartSql.Cache.Redis](https://img.shields.io/nuget/v/SmartSql.Cache.Redis.svg)](https://www.nuget.org/packages/SmartSql.Cache.Redis/)  | [![SmartSql.Cache.Redis](https://img.shields.io/nuget/dt/SmartSql.Cache.Redis.svg)](https://www.nuget.org/packages/SmartSql.Cache.Redis/) |
| [SmartSql.ZooKeeperConfig](https://www.nuget.org/packages/SmartSql.ZooKeeperConfig/) | [![SmartSql.ZooKeeperConfig](https://img.shields.io/nuget/v/SmartSql.ZooKeeperConfig.svg)](https://www.nuget.org/packages/SmartSql.ZooKeeperConfig/)  | [![SmartSql.ZooKeeperConfig](https://img.shields.io/nuget/dt/SmartSql.ZooKeeperConfig.svg)](https://www.nuget.org/packages/SmartSql.ZooKeeperConfig/) |

## 0. Why

- 拥抱 跨平台 DotNet Core，是时候了。
- 高性能、高生产力，超轻量级的ORM。**107kb**

---

## 1. So SmartSql

- TargetFrameworks: .NETFramework 4.6 & .NETStandard 2.0
- SmartSql = MyBatis + Cache(Memory | Redis) + ZooKeeper + R/W Splitting + ......

---

## 2. 主要特性

- 1 ORM
  - 1.1 Sync
  - 1.2 Async
- 2 XmlConfig & XmlStatement -> Sql
  - 2.1 SmartSqlMapConfig & SmartSqlMap (是的，你猜对了，和MyBatis一样，通过XML配置分离SQL。)
  - 2.2 Config Hot Update ->ConfigWatcher & Reload (配置文件热更新：当你需要修改Sql的时候，直接修改SqlMap配置文件，保存即可。)
- 3 读写分离
  - 3.1 读写分离
  - 3.2 多读库 权重筛选 （配置多读库，根据读库权重选举读库）
- 4 日志
  - 4.1 基于 Microsoft.Extensions.Logging.Abstractions  (当你需要跟踪调试的时候一切都是那么一目了然)
- 5 Dynamic Repository
  - 5.1 SmartSql.DyRepository  （解放你的双手，你来定义仓储接口，我来实现数据库访问）
- 6 查询缓存  （热数据缓存，一个配置轻松搞定）
  - 6.1 SmartSql.Cache.Memory
    - 6.1.1 Fifo
    - 6.1.2 Lru
  - 6.2 SmartSql.Cache.Redis
  - 6.3 缓存事务一致性
- 7 分布式配置插件
  - 7.1 IConfigLoader (配置文件加载器)
  - 7.2 LocalFileConfigLoader  (本地文件配置加载器)
    - 7.2.1 Load SmartSqlMapSource Xml
    - 7.3.1 Load SmartSqlMapSource Directory
  - 7.3 SmartSql.ZooKeeperConfig (ZooKeeper 分布式配置文件加载器)

---

## 3. 性能评测

``` ini

BenchmarkDotNet=v0.10.14, OS=Windows 10.0.17134
Intel Core i7-6700K CPU 4.00GHz (Skylake), 1 CPU, 8 logical and 4 physical cores
.NET Core SDK=2.1.201
  [Host]     : .NET Core 2.0.7 (CoreCLR 4.6.26328.01, CoreFX 4.6.26403.03), 64bit RyuJIT
  DefaultJob : .NET Core 2.0.7 (CoreCLR 4.6.26328.01, CoreFX 4.6.26403.03), 64bit RyuJIT


```
|            ORM |                     Type |                  Method |        Return |      Mean |     Error |    StdDev | Rank |     Gen 0 |     Gen 1 |     Gen 2 | Allocated |
|--------------- |------------------------- |------------------------ |-------------- |----------:|----------:|----------:|-----:|----------:|----------:|----------:|----------:|
|         Native |         NativeBenchmarks |   Query_GetValue_DbNull | IEnumerable`1 |  78.39 ms | 0.8935 ms | 0.7921 ms |    1 | 3000.0000 | 1125.0000 |  500.0000 |  15.97 MB |
|       SmartSql |       SmartSqlBenchmarks |                   Query | IEnumerable`1 |  78.46 ms | 0.2402 ms | 0.1875 ms |    1 | 2312.5000 | 1000.0000 |  312.5000 |  12.92 MB |
| SmartSqlDapper | SmartSqlDapperBenchmarks |                   Query | IEnumerable`1 |  78.65 ms | 1.2094 ms | 1.1312 ms |    1 | 3687.5000 | 1437.5000 |  687.5000 |  19.03 MB |
|         Native |         NativeBenchmarks | Query_IsDBNull_GetValue | IEnumerable`1 |  78.84 ms | 0.8984 ms | 0.7502 ms |    1 | 2312.5000 | 1000.0000 |  312.5000 |  12.92 MB |
|         Dapper |         DapperBenchmarks |                   Query | IEnumerable`1 |  79.00 ms | 1.0949 ms | 0.9706 ms |    1 | 3312.5000 | 1312.5000 |  625.0000 |  17.19 MB |
|             EF |             EFBenchmarks |                   Query | IEnumerable`1 |  79.44 ms | 1.6880 ms | 1.5789 ms |    1 | 6250.0000 |         - |         - |  26.05 MB |
|       SqlSugar |       SqlSugarBenchmarks |                   Query | IEnumerable`1 |  81.09 ms | 0.8718 ms | 0.7728 ms |    2 | 2187.5000 |  875.0000 |  250.0000 |  12.64 MB |
|          Chloe |          ChloeBenchmarks |                   Query | IEnumerable`1 |  83.86 ms | 1.2714 ms | 1.1893 ms |    3 | 2250.0000 |  937.5000 |  312.5000 |  12.62 MB |
|             EF |             EFBenchmarks |                SqlQuery | IEnumerable`1 |  89.11 ms | 0.7562 ms | 0.6314 ms |    4 | 8187.5000 |  125.0000 |         - |  33.68 MB |
|             EF |             EFBenchmarks |        Query_NoTracking | IEnumerable`1 |  93.13 ms | 0.8458 ms | 0.7912 ms |    5 | 5875.0000 | 2250.0000 | 1062.5000 |  29.71 MB |
|             EF |             EFBenchmarks |     SqlQuery_NoTracking | IEnumerable`1 | 106.89 ms | 1.0998 ms | 1.0288 ms |    6 | 7437.5000 | 2875.0000 | 1312.5000 |  37.34 MB |

---

## 4. 安装 (NuGet)

``` csharp
Install-Package SmartSql
```

## 5. 常规代码

### 查询

``` csharp
            ISmartSqlMapper SqlMapper = MapperContainer.Instance.GetSqlMapper();
            SqlMapper.Query<T_Test>(new RequestContext
            {
                Scope = "T_Test",
                SqlId = "GetList",
                Request = new { Ids = new long[] { 1, 2, 3, 4 } }
            });
```

### 事务

``` csharp
            try
            {
                ISmartSqlMapper SqlMapper = MapperContainer.Instance.GetSqlMapper();
                SqlMapper.BeginTransaction();
                //BizCode
                SqlMapper.CommitTransaction();
            }
            catch (Exception ex)
            {
                SqlMapper.RollbackTransaction();
                throw ex;
            }
```

## 6. 最佳实践

### 6.1 安装 SmartSql.DIExtension

``` chsarp
Install-Package SmartSql.DIExtension
```

### 6.2 注入依赖

``` csharp
 services.AddSmartSql();
 services.AddRepositoryFactory();
 services.AddRepositoryFromAssembly((options) =>
 {
    options.AssemblyString = "SmartSql.Starter.Repository";
 });
```

### 6.3 定义仓储接口

``` csharp
    /// <summary>
    /// 属性可选： [SqlMap(Scope = "User")] ,不设置 则默认 Scope 模板：I{Scope}Repository
    /// 可传入自定义模板
    /// RepositoryBuilder builder=new RepositoryBuilder("I{Scope}DAL");
    /// </summary>
    public interface IUserRepository
    {
        /// <summary>
        /// 属性可选 [Statement(Execute = ExecuteBehavior.Auto,Id = "Query")]
        /// 默认 Execute：Auto ，自动判断 执行类型
        /// 默认 Id : 方法名
        /// </summary>
        /// <param name="reqParams"></param>
        /// <returns></returns>
        IEnumerable<User> Query(object reqParams);
        long GetRecord(object reqParams);
        User Get(object reqParams);
        long Insert(User entity);
        int Update(User entity);
        int Delete(User enttiy);
    }
```

### 6.4 尽情享用

``` csharp
    public class UserService
    {
        private readonly ISmartSqlMapper _smartSqlMapper;
        private readonly IUserRepository _userRepository;

        public UserService(
             ISmartSqlMapper smartSqlMapper
            , IUserRepository userRepository)
        {
            _smartSqlMapper = smartSqlMapper;
            _userRepository = userRepository;
        }

        public long Add(AddRequest request)
        {
            int existsNum = _userRepository.Exists(new { request.UserName });
            if (existsNum > 0)
            {
                throw new ArgumentException($"{nameof(request.UserName)} has already existed!");
            }
            return _userRepository.Add(new Entitiy.User
            {
                UserName = request.UserName,
                Password = request.Password,
                Status = Entitiy.UserStatus.Ok,
                CreationTime = DateTime.Now,
            });
        }

        public void UseTransaction()
        {
            try
            {
                _smartSqlMapper.BeginTransaction();
                //Biz();
                _smartSqlMapper.CommitTransaction();
            }
            catch (Exception ex)
            {
                _smartSqlMapper.RollbackTransaction();
                throw ex;
            }
        }
    }
```

## 7. 文档地址

- [在线阅读地址](https://doc.smartsql.net/)
- [PDF](https://www.gitbook.com/download/pdf/book/ahoo-wang/smartsql-doc-cn)
- [Mobi](https://www.gitbook.com/download/mobi/book/ahoo-wang/smartsql-doc-cn)
- [ePub](https://www.gitbook.com/download/epub/book/ahoo-wang/smartsql-doc-cn)

## 8. 技术交流

点击链接加入QQ群【SmartSql 官方交流群】：[604762592](https://jq.qq.com/?_wv=1027&k=5Sy8Ahw)