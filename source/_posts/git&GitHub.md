---
title: git&GitHub&Gitee入门讲解
date: 2025-01-07 17:19:00
tags:
  - 基础知识
categories: git
photos: /tupian/git1.png
---

# **Git、GitHub 和 Gitee 完整讲解：从基础到进阶功能**

---

## **1. 前言**

本教程详细讲解 Git、GitHub 和 Gitee 的使用，从基础到进阶，帮助开发者全面掌握这三者的功能与应用。

---

## **2. 第一部分：Git 是什么？**

### **2.1 比喻：Git 就像一本“时光机日记本” 📖**

- 每一段代码的改动，Git 都会记录下来，像是在写日记。
- 如果代码出现问题，Git 可以“穿越回过去”，恢复到任意时间点的状态。

### **2.2 Git 的主要特点**

1. **版本控制**：每次提交都像写了一篇新日记，保存开发成果。
2. **分支管理**：分支就像章节，可以并行开发而互不干扰。
3. **分布式**：每个人都拥有完整的“时光机日记本”，即便离线也能工作。

---

## **3. 第二部分：GitHub 和 Gitee 是什么？**

### **3.1 GitHub：全球化的代码社交云平台 🌐**

- **比喻**：GitHub 是“全球代码图书馆”。
- **优势**：
  - 开源社区庞大，适合学习和参与开源项目。
  - 是开发者协作开发的最佳平台。

### **3.2 Gitee：中国本地化的代码托管平台 🇨🇳**

- **比喻**：Gitee 是 GitHub 的“中国版伙伴”。
- **优势**：
  - 对国内开发者友好，速度快。
  - 与钉钉、企业微信等本地工具无缝集成。
  - 常用于企业内部项目或私有化部署。

---

## **4. 第三部分：Git 常用命令及 SSH 配置**

### **4.1 SSH：安全认证和便捷连接 🔒**

- **比喻**：SSH 就像“为钥匙加上指纹认证”，确保只有你能开门。
- **功能**：
  - 在本地和远程仓库之间实现安全通信。
  - 免去每次推送或拉取代码时输入密码的麻烦。

### **4.2 Git 常用命令速查表**

| 功能               | 命令                                                                              | 比喻                                       |
| ------------------ | --------------------------------------------------------------------------------- | ------------------------------------------ |
| 配置用户名和邮箱   | `git config --global user.name "名字"`<br>`git config --global user.email "邮箱"` | 设置“署名”，每次提交都会标明是谁的贡献。   |
| 初始化仓库         | `git init`                                                                        | 新建一本“时光机日记本”，准备开始记录版本。 |
| 添加文件到暂存区   | `git add 文件名`                                                                  | 把草稿整理好，放到“草稿区”。               |
| 提交到本地仓库     | `git commit -m "提交说明"`                                                        | 把草稿正式写进日记本，并附上说明。         |
| 推送代码到远程仓库 | `git push origin 分支名`                                                          | 同步本地代码到远程仓库。                   |
| 克隆远程仓库       | `git clone 仓库地址`                                                              | 下载别人的代码到本地。                     |
| 查看状态           | `git status`                                                                      | 检查当前代码的变化情况。                   |
| 查看提交历史       | `git log`                                                                         | 查看提交记录，回顾开发“时间线”。           |
| 创建分支           | `git branch 分支名`                                                               | 为不同功能创建独立章节。                   |
| 切换分支           | `git checkout 分支名`                                                             | 从一个章节切换到另一个章节。               |
| 合并分支           | `git merge 分支名`                                                                | 把不同章节内容合并到主线。                 |
| 拉取代码           | `git pull origin 分支名`                                                          | 从远程仓库拉取最新代码。                   |

### **4.3 SSH 配置步骤**

1. **配置个人信息**
   ```bash
   git config --global user.name "你的名字"
   git config --global user.email "你的邮箱"
   ```
2. **生成 SSH 密钥**
   ```bash
   ssh-keygen -t rsa -C "你的邮箱"
   ```
3. **添加公钥到远程仓库**

- **GitHub**：

  1. 打开 `Settings`。
  2. 选择 `SSH and GPG keys`。
  3. 点击 `New SSH key`。
  4. 粘贴公钥内容并保存。

- **Gitee**：
  1. 打开 `设置`。
  2. 选择 `安全设置`。
  3. 点击 `SSH 公钥`。
  4. 粘贴公钥内容并保存。

4. **测试连接**
   ```bash
   ssh -T git@github.com
   ssh -T git@gitee.com
   ```

- 成功连接时会显示欢迎信息，如：
  ```vbnet
  Hi username! You've successfully authenticated, but GitHub does not provide shell access.
  ```

5. **配置多个 SSH 密钥（可选）**

- 如果你需要同时管理多个远程仓库（如 GitHub 和 Gitee），可以为每个仓库配置不同的 SSH 密钥。
- 1.生成额外的 SSH 密钥：
  ```bash
  ssh-keygen -t rsa -C "另一个邮箱"
  ```
  - 保存为不同路径（如 ~/.ssh/id_rsa_gitee）。
- 2.编辑 SSH 配置文件： 创建或编辑 ~/.ssh/config 文件，添加以下内容：

  ```bash
  Host github.com
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_rsa

  Host gitee.com
      HostName gitee.com
      User git
      IdentityFile ~/.ssh/id_rsa_gitee
  ```

- 3.测试连接： 确保两者都可以成功连接：
  ```bash
  ssh -T git@github.com
  ssh -T git@gitee.com
  ```

## **5. 第四部分：GitHub 和 Gitee 的核心功能详解**

| 功能         | GitHub                               | Gitee                  |
| ------------ | ------------------------------------ | ---------------------- |
| Fork         | 复制项目到个人账户                   | 同样支持复制项目。     |
| Star         | 收藏项目，便于以后查找               | 同样支持收藏项目。     |
| Watch        | 订阅项目动态                         | 支持动态订阅。         |
| Issues       | 提交问题或建议，记录开发中的待办事项 | 问题追踪更加强本地化。 |
| Pull Request | 提交代码修改供原项目合并             | 提供类似功能。         |
| Actions      | 自动化 CI/CD 工作流                  | 不支持此功能。         |
| Pages        | 托管静态网站（如博客或文档）         | 提供类似功能。         |
| Releases     | 发布稳定版本，提供下载               | 同样支持发布功能。     |
| Webhooks     | 自动消息通知                         | 支持类似功能。         |

## **6. 第五部分：总结与对比**

### **6.1 Git：核心工具**

- Git 是一个版本管理工具，用于记录代码修改历史、创建和合并分支等。

### **6.2 GitHub 和 Gitee：平台对比**

- GitHub：全球化，功能丰富，适合开源项目和国际化协作。
- Gitee：本地化，速度快，适合国内团队和企业。

## **本片文章只是带着你们了解以及会用，精通还需个人**
