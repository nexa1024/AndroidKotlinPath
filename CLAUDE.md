# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

AndroidKotlinPath 是一个 Android 开发教育项目，通过 10 个渐进式实验室（Lab）教授 Android 核心技术和 Kotlin 语言。项目采用单一应用架构，将所有 Lab 整合到一个 App 中，主界面通过 RecyclerView 显示 Lab 1-10 的导航列表。

## 构建命令

### 标准构建
```bash
# 构建 Debug APK
./gradlew assembleDebug

# 构建 Release APK
./gradlew assembleRelease

# 安装 Debug 版本到连接的设备/模拟器
./gradlew installDebug

# 清理构建
./gradlew clean
```

### 运行测试
```bash
# 运行单元测试
./gradlew test

# 运行设备测试（需要连接设备/模拟器）
./gradlew connectedAndroidTest

# 运行特定测试类
./gradlew test --tests "com.nexa.androidkotlinpath.ExampleUnitTest"
```

### 代码质量检查
```bash
# 运行 Lint 检查
./gradlew lint

# 生成 Lint 报告
./gradlew lintDebug
```

## 项目架构

### 单应用多 Lab 架构
项目采用统一架构，所有 10 个 Lab 都在同一个应用（`com.nexa.androidkotlinpath`）中。每个 Lab 都可以通过主导航屏幕访问。

### 包结构
```
com.nexa.androidkotlinpath/
├── MainActivity.kt              # 主入口，包含 RecyclerView 用于 Lab 导航
├── ui/                          # UI 组件
│   ├── lab1/                    # Lab 1: Hello World
│   ├── lab2/                    # Lab 2: UI 基础
│   ├── lab3/                    # Lab 3: Activity 与 Intent
│   ├── lab4/                    # Lab 4: Fragment 与 RecyclerView
│   ├── lab5/                    # Lab 5: 数据存储
│   ├── lab6/                    # Lab 6: Service 与后台任务
│   ├── lab7/                    # Lab 7: 网络编程
│   ├── lab8/                    # Lab 8: ContentProvider
│   ├── lab9/                    # Lab 9: 权限与系统特性
│   └── lab10/                   # Lab 10: 综合项目
├── data/                        # 数据层（后续 Lab 使用）
├── model/                       # 数据模型
└── utils/                       # 工具函数
```

### Gradle 配置
- **Kotlin 版本**: 2.0.21
- **AGP 版本**: 8.13.1
- **编译 SDK**: 36
- **最低 SDK**: 33
- **目标 SDK**: 36
- **命名空间**: `com.nexa.androidkotlinpath`

### 版本目录（gradle/libs.versions.toml）
项目使用 Gradle 版本目录管理依赖。所有库版本都集中在 `libs.versions.toml` 中管理。

## 核心技术栈

### 核心库
- **Kotlin**: 主要开发语言
- **AndroidX Core KTX**: Android 的 Kotlin 扩展
- **Appcompat**: 向后兼容支持
- **Material Design**: UI 组件
- **ConstraintLayout**: 高级布局
- **Activity**: 现代 Activity API

### 构建配置
- **Kotlin DSL**: 所有构建脚本使用 `.kts` 文件
- **版本目录**: 集中式依赖管理
- **阿里云镜像**: 在 `settings.gradle.kts` 中配置了中国镜像以加快构建速度

## Lab 学习结构

每个 Lab 遵循标准结构：
1. **学习目标**（3-5 个）
2. **理论知识**（30%）：核心概念、Kotlin 特性、最佳实践
3. **代码示例**（40%）：基础和进阶示例
4. **实践任务**（30%）：必做题（2-3 个）+ 挑战题（1 个）
5. **验收标准**: 完成检查清单

### Lab 进阶路线
- **Lab 1-3**: 基础入门（环境搭建、UI、Activity/Intent）
- **Lab 4-6**: 核心组件（Fragment、数据存储、Service）
- **Lab 7-8**: 网络与数据（HTTP、ContentProvider）
- **Lab 9-10**: 系统功能（权限、综合项目）

## 文档结构

- **README.md**: 项目概览和学习路径摘要
- **docs/index.md**: 详细学习指南（博客格式，带 frontmatter）
- **docs/Lab1-HelloWorld.md**: 各个 Lab 的详细文档
- **docs/template.md**: 创建新 Lab 文档的模板

`docs/` 中的所有文档文件使用 YAML frontmatter 以便集成到博客：
```yaml
---
title: Lab 标题
date: YYYY-MM-DD
categories: Android
---
```

## 开发流程

### 添加新 Lab
1. 在相应的包中创建 Activity：`ui/labX/`
2. 在 `res/layout/` 中添加布局 XML
3. 在 `AndroidManifest.xml` 中注册
4. 在主 RecyclerView adapter 中添加条目
5. 使用模板在 `docs/LabX-Title.md` 中创建文档
6. 如需要，更新 `README.md`

### 导航模式
主屏幕使用 RecyclerView 显示所有 10 个 Lab。点击 Lab 条目通过 Intent 导航到对应 Lab 的 Activity。

## 重要说明

- **不是独立项目**: 所有 Lab 在一个应用中，而不是 10 个独立项目
- **纯 Kotlin 开发**: 只使用 Kotlin，不包含 Java 代码
- **现代 Android**: 使用最新的 Android API 和最佳实践
- **教育优先**: 代码优先考虑清晰度而非性能优化
- **渐进式复杂度**: 每个 Lab 都基于前面的知识

## 常见问题

### 构建错误
- 如果同步失败，检查 Gradle wrapper 版本是否与 `gradle-wrapper.properties` 匹配
- 中国用户：确保 `settings.gradle.kts` 中的阿里云镜像正常工作
- 清理构建：`./gradlew clean` 通常能解决缓存问题

### 添加依赖
先添加到 `gradle/libs.versions.toml`，然后在 `app/build.gradle.kts` 中引用：
```kotlin
implementation(libs.libraryName)
```

## 测试策略

- **单元测试**: 位于 `app/src/test/`
- **设备测试**: 位于 `app/src/androidTest/`
- **测试运行器**: AndroidJUnitRunner
- **测试库**: JUnit 4, Espresso, androidx.test.ext.junit

## 中文环境支持

项目已配置阿里云 Maven 镜像以加速依赖下载：
- 插件仓库：`https://maven.aliyun.com/repository/google`
- 库仓库：`https://maven.aliyun.com/repository/public`

这些镜像在 `settings.gradle.kts` 的 `pluginManagement` 和 `dependencyResolutionManagement` 块中配置。
