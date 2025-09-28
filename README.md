# godot-cpp 模板
这个仓库是用于 Godot 4.0+ 的 GDExtension 开发的快速入门模板。

## 内容
* 一个空的Godot项目 (`demo/`)
* godot-cpp作为一个子模块 (`godot-cpp/`)
* GitHub Issues 模板 (`.github/ISSUE_TEMPLATE.yml`)
* GitHub CI/CD 工作流：在创建 Release 时自动发布你的库包(`.github/workflows/builds.yml`)
* 预置的C++源码文件: 用于开发GDExtension(位于src/目录)
* 自动生成设置:会在doc_classes/目录下生成.xml文件，供Godot解析为GDExtension内置文档

## 用法 - 模板

要使用此模板，请登录 GitHub 并在仓库页面顶部点击绿色的“使用此模板”按钮。(创建这个仓库的分支)
这将让您创建此仓库的副本，且具有干净的 Git 历史记录。请确保克隆正确的分支，因为这些分支针对各自的 Godot 开发分支进行了配置，并且彼此不同。请参考文档以了解各版本之间的差异。

在将自己的分支克隆到本地之后，您应该开始：
* 通过 `git submodule update --init` 初始化git子模块
* 更改动态库的名字
  * 可以通过修改`libname`字符串来改变`SConstruct`文件中编译的动态库文件的名称。
  * 可以在项目路径的demo/bin/example.gdextension文件中修改各个平台要加载的动态库的路径名，里面的`EXTENSION-NAME`字段需要替换为`SConstruct`文件中指定的名称。
  * 可以更改这个`demo/bin/example.gdextension`文件的名称
* 可以修改`demo/bin/example.gdextension`文件中的`entry_symbol`字段对应的内容,使其与你的GDExtension项目中`export "c"`块中的`GDExtensionBool GDE_EXPORT`修饰符的函数名称相匹配,这个决定了你的GDExtension的入口函数(或者说是加载函数),使其能够被Godot编辑器的C API加载
* 在`register_types.cpp`文件中的初始化方法`initialize_gdextension_types`中, 可以使用`GDREGISTER_CLASS(CLASS_NAME);`来注册你自己实现的类

### 配置集成开发环境
你可以使用任何文本编辑器编写扩展，并通过命令行调用 SCons 进行构建；但如果想借助 IDE（集成开发环境），只需提供一个名为 compile_commands.json 的编译数据库文件。大多数 IDE 会自动识别该文件并完成相应的配置
要在项目根目录生成该数据库文件，可运行以下任一命令:
```shell
# 在编译的同时生成 compile_commands.json
scons compiledb=yes

# 仅生成 compile_commands.json，不进行编译
scons compiledb=yes compile_commands.json
```

## 用法 - Actions

本仓库已内置 GitHub Actio, 可跨平台构建GDExtension, 并在每次推送时自动触发。你可前往`.github/workflows/builds.yml`查看或修改配置。
工作流运行结束后，可在 GitHub 的 Actions 标签页中下载生成的`godot-cpp-template.zip`文件。
