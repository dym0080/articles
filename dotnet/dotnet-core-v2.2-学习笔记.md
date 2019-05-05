
> [dotnet core2.2学习来源](https://docs.microsoft.com/zh-cn/aspnet/core/?view=aspnetcore-2.2)


## Razor Pages页面筛选器 VS  ASP.NET Core MVC Action筛选器

[Razor Pages页面筛选器](https://docs.microsoft.com/zh-cn/aspnet/core/razor-pages/filter?view=aspnetcore-2.2)
- 实现`IPageFilter` 或 `IAsyncPageFilter` 接口

[ASP.NET Core MVC Action筛选器](https://docs.microsoft.com/zh-cn/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.2#action-filters)
- 实现 `IActionFilter` 或 `IAsyncActionFilter` 接口
- 它们的执行围绕着操作方法的执行s

## 弱类型数据（`ViewData`、`ViewData` 属性和 `ViewBag`）

- `ViewBag` 在 Razor 页中不可用。对于 `ViewData` 和 `ViewBag`，键查找都不区分大小写。`ViewData` 和 `ViewBag` 在运行时进行动态解析。 由于它们不提供编译时类型检查，因此使用这两者通常比使用 viewmodel 更容易出错。 出于上述原因，一些开发者希望尽量减少或根本不使用 `ViewData` 和 `ViewBag`。

- 三者之间的区别

## 视图 VS 分部视图 VS 视图组件

- 分部视图的文件名通常以下划线 (`_`) 开头。 虽然未强制要求遵从此命名约定，但它有助于直观地将分部视图与视图和页面区分开来。

## 中间件
- [ASP.NET Core 中间件详解及项目实战](https://www.cnblogs.com/savorboard/p/5586229.html)