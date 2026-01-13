# Wails 模板

## 介绍

这是一个 Wails 开发桌面应用模板, 前端使用 NextJs 16.1 + Shadcn ui

## 改动

NextJs 默认输入到 `.next`, 改为输出到 `dist`  
已添加大量 shadcn ui 默认组件

```ts
// frontend/next.config.ts 添加 distDir 指定输出路径
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  /* config options here */
  distDir: "dist",
  output: "export",
  trailingSlash: true,
  images: {
    unoptimized: true,
  },
};

export default nextConfig;
````



golang 默认嵌入 `//go:embed all:frontend/dist`, 改为 `//go:embed all:frontend/dist/build`  
NextJs 16 会生成 lock 文件锁定进程, golang 无法嵌入

```go
// wails dev 模式下 main.go 修改嵌入路径为 frontend/dist/build

//go:embed all:frontend/dist/build
var assets embed.FS


// wails build 模式下 main.go 还原嵌入路径为 frontend/dist

//go:embed all:frontend/dist
var assets embed.FS
````

## 快速使用

```bash
 # 开发模式, 支持热更新
 $ wails dev
 
 # 构建桌面应用
 $ wails build
```
