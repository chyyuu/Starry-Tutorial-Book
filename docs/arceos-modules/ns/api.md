# 模块接口与用例

## 管理命名空间

### [`AxNamespace::global`](https://arceos.org/arceos/axns/struct.AxNamespace.html#method.global)

获取全局命名空间。实际上获取的是 `axns_resource` 段的地址。

### [`Axnamespace::new_thread_local`](https://arceos.org/arceos/axns/struct.AxNamespace.html#method.new_thread_local)

新建一个线程本地命名空间。分配了一块内存区域并拷贝全局命名空间。

### [`AxNamespaceIf::current_namespace_base`](https://arceos.org/arceos/axns/trait.AxNamespaceIf.html#tymethod.current_namespace_base)

需要调用者通过 [`#[crate_interface::impl_interface]`](https://docs.rs/crate_interface/latest/crate_interface/attr.impl_interface.html) 提供的方法。获取当前线程命名空间的基地址。

例如在 Starry 中，我们把用户程序的命名空间保存在 `TaskExt` 中，就需要在这里实现获取当前 `TaskExt` 并返回命名空间的基地址的逻辑。

## 注册资源

### [`def_resource!`](https://arceos.org/arceos/axns/macro.def_resource.html)

通过 `def_resource!` 宏定义可被命名空间管理的资源。该宏把资源链接到 `axns_resource` 段中，由此计算资源存储在命名空间中的偏移，并实现一系列解引用方法。

### [`ResArc<T>`](https://arceos.org/arceos/axns/struct.ResArc.html)

对 `LazyInit<Arc<T>>` 的简单封装，用于懒惰初始化资源。

## 例子

```rust
use axns::ResArc;

axns::def_resource! {
    static FOO: u32 = 42;
    static BAR: ResArc<String> = ResArc::new();
}

BAR.init_new("hello world".to_string());
assert_eq!(*FOO, 42);
assert_eq!(BAR.as_str(), "hello world");
```
