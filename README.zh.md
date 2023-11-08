中文 | [English](./README.md)

# Tamagui + Solito + Next + Expo ReactNaive + Jotai

## 🔦 关于

这是一个基于 Expo + Next.js + Tamagui + Solito 应用程序的起步演示项目。

## 📦 包括的包

- [Tamagui](https://tamagui.dev)
- [Solito](https://solito.dev) 用于跨平台导航
- [Jotai](https://jotai.org)
- Expo SDK
- Next.js
- Expo Router

## 🗂 文件布局

主要的应用程序有:

- `expo` (原生)
- `next` (网页)

- `packages` 跨应用程序共享的包
  - `ui` 包含将由 Tamagui 优化的自定义 UI 套件
  - `app` 你将从 `app/` 导入大多数文件
    - `features` (不使用 `screens` 文件夹，按功能组织)
    - `provider` (包裹应用程序的所有提供者，以及一些 Web 的无操作)

如果你知道你在做什么并且有充分的理由，你可以在 `packages/` 中添加其他文件夹。

## 🏁  启动应用程序

- 安装依赖项: `yarn`

- Next.js 本地开发: `yarn web`

要在开发模式下运行优化器（仅用于测试，关闭它会更快）：`yarn web:extract`。为生产环境构建 `yarn web:prod`。

要查看编译器的调试输出，请在任何文件的顶部添加 `// debug` 作为注释。

- Expo 本地开发: `yarn native`

## UI 套件

注意我们正在遵循 [设计系统指南](https://tamagui.dev/docs/guides/design-systems) 并为组件创建我们自己的包

查看 `packages/ui` 命名为 `@my/ui` 的内容，了解这是如何工作的。

## 🆕 添加新依赖项

### 纯 JS 依赖项

如果你要安装一个将跨平台使用的只有 JavaScript 的依赖项，请在 `packages/app` 中安装它

```sh
cd packages/app
yarn add date-fns
cd ../..
yarn
```

### 原生依赖项

如果你要安装包含任何原生代码的库，必须在 `expo` 中安装它：

```sh
cd apps/expo
yarn add react-native-reanimated
cd ..
yarn
```

## 更新新依赖项

### 纯 JS 依赖项

```sh
yarn upgrade-interactive
```

你也可以在 `packages/app` 中安装原生库，如果你想在 `app` 文件夹内自动导入该包。但是，你需要小心并安装完全相同版本的两个包。如果版本有任何不匹配，你可能会遇到严重的错误。这是一个经典的 monorepo 问题。我使用 `lerna-update-wizard` 来帮助这个（你不需要使用 Lerna 来使用那个库）。

你可能还想让 next 应用程序的原生模块进行转译。如果你看到 `Cannot use import statement outside a module` 的错误信息，你可能需要在 `next.config.js` 中使用 `transpilePackages` 并将模块添加到那里的数组中。


## 部署到 Vercel

- 根目录: `apps/next`
- 安装命令为 `yarn set version stable && yarn install`
- 构建命令：保留默认设置
- 输出目录：保留默认设置

### Vercel 部署故障排除
如果在推送到 GitHub 后，你看到自动的 vercel 部署失败，错误信息如下：
```
➤ YN0028: │ The lockfile would have been modified by this install, which is explicitly forbidden.
➤ YN0000: └ Completed
➤ YN0000: Failed with errors in 0s 700ms
Error: Command "yarn set version stable && yarn install" exited with 1
```
在本地运行 yarn vercel:install 然后提交并推送更改到 GitHub。
