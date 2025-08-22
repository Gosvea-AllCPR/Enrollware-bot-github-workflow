# Enrollware Bot

自动化 Enrollware 学生数据导出工具，支持云端部署和 Google Drive 集成。

## 🚀 功能特性

- **自动登录**: 智能处理 Enrollware 系统身份验证
- **智能日期选择**: 自动导出最近 30 天的数据
- **Excel 导出**: 将学生数据导出为 Excel 格式 (.xlsx)
- **云端部署**: 支持 GitHub Actions 自动化每日运行
- **Google Drive 集成**: 可选的自动上传到 Google Drive
- **错误处理**: 强大的错误处理机制，失败时自动截图
- **灵活输入**: 支持粘贴和逐字符输入，提高兼容性

## 📋 系统要求

- Node.js 18 或更高版本
- Google Chrome 浏览器（本地运行时需要）
- 有效的 Enrollware 账户凭证

## 🔧 本地安装

1. **克隆仓库：**
   ```bash
   git clone https://github.com/your-username/enrollware-bot.git
   cd enrollware-bot
   ```

2. **安装依赖：**
   ```bash
   npm install
   ```

3. **配置环境变量：**
   在根目录创建 `.env` 文件：
   ```env
   EW_USER=你的_enrollware_用户名
   EW_PASS=你的_enrollware_密码
   
   # 可选：Google Drive 集成
   GOOGLE_DRIVE_CREDENTIALS={"type":"service_account",...}
   GOOGLE_DRIVE_FOLDER_ID=你的文件夹ID
   ```

4. **运行脚本：**
   ```bash
   npm start
   ```

## ☁️ 云端部署 (GitHub Actions)

### 1. 仓库设置

1. 创建新的 GitHub 仓库
2. 将代码推送到仓库：
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/你的用户名/enrollware-bot.git
   git push -u origin main
   ```

### 2. 配置 GitHub Secrets

前往仓库的 **Settings > Secrets and variables > Actions** 并添加：

#### 必需的 Secrets：
- `EW_USER`: 你的 Enrollware 用户名
- `EW_PASS`: 你的 Enrollware 密码

#### 可选的（Google Drive）：
- `GOOGLE_DRIVE_CREDENTIALS`: Google Drive API 服务账户 JSON 凭证
- `GOOGLE_DRIVE_FOLDER_ID`: 目标 Google Drive 文件夹 ID

### 3. Google Drive 设置（可选）

#### 3.1 创建 Google Cloud 项目
1. 访问 [Google Cloud Console](https://console.cloud.google.com/)
2. 创建新项目或选择现有项目
3. 启用 Google Drive API

#### 3.2 创建服务账户
1. 前往 IAM 和管理 > 服务账户
2. 创建新的服务账户
3. 下载 JSON 密钥文件
4. 将 JSON 内容复制到 `GOOGLE_DRIVE_CREDENTIALS` secret

#### 3.3 获取文件夹 ID
1. 在 Google Drive 中创建目标文件夹
2. 从 URL 中获取文件夹 ID（URL 中的长字符串）
3. 将其添加到 `GOOGLE_DRIVE_FOLDER_ID` secret

### 4. 自动化调度

配置完成后，脚本将：
- 每天凌晨 2:00 UTC 自动运行
- 导出最近 30 天的学生数据
- 上传文件到 Google Drive（如果已配置）
- 将文件存储为 GitHub Actions 工件

## 🎯 手动执行

你可以手动触发工作流：
1. 前往仓库的 **Actions** 标签页
2. 选择 "Enrollware Data Export" 工作流
3. 点击 "Run workflow"

## 📁 项目结构

```
enrollware-bot/
├── .github/workflows/
│   └── export.yml          # GitHub Actions 工作流
├── chrome-data/             # Chrome 用户数据目录
├── downloads/               # 下载文件目录
├── enrollware-bot/
│   └── upload-to-drive.js   # Google Drive 上传功能
├── login_and_export.js      # 主脚本
├── package.json             # 依赖和脚本
├── DEPLOYMENT.md            # 部署指南
└── README.md               # 英文说明文件
```

## 🔍 工作原理

1. **身份验证**: 脚本导航到 Enrollware 并自动处理登录
2. **日期配置**: 设置自定义日期范围（最近 30 天）
3. **导出过程**: 配置导出设置并触发下载
4. **文件管理**: 监控下载完成并管理文件
5. **上传**: 可选择上传文件到 Google Drive
6. **清理**: 处理错误和清理过程

## 🛠️ 故障排除

### 常见问题：

1. **Chrome 启动失败**: 
   - 检查 Chrome 安装路径
   - 验证环境变量中的 Chrome 二进制位置

2. **登录失败**: 
   - 验证 secrets/环境中的用户名和密码
   - 检查是否有验证码或额外安全措施

3. **Google Drive 上传失败**: 
   - 验证 API 凭证格式
   - 检查文件夹 ID 和权限
   - 确保服务账户有访问文件夹的权限

4. **文件下载失败**: 
   - 检查网络连接
   - 验证 Enrollware 网站结构是否有变化

### 调试方法：

1. 查看 GitHub Actions 日志获取详细错误信息
2. 使用手动工作流触发进行测试
3. 检查环境变量配置
4. 查看错误截图（失败时自动捕获）

## 🔒 安全注意事项

- 切勿将敏感凭证提交到仓库
- 定期更新密码和 API 密钥
- 为 Google Drive API 使用最小权限
- 监控 GitHub Actions 使用情况和日志
- 保持依赖项更新

## 📊 依赖项

- **puppeteer-real-browser**: ^1.0.0 - 浏览器自动化
- **dotenv**: ^16.0.0 - 环境变量管理
- **googleapis**: ^128.0.0 - Google Drive API 集成

## 📄 许可证

MIT 许可证 - 详情请查看 LICENSE 文件。

## 👨‍💻 作者

**Boyi Wang**  
邮箱: [boyiwanglance@gmail.com](mailto:boyiwanglance@gmail.com)

## 🤝 贡献

1. Fork 仓库
2. 创建功能分支
3. 提交更改
4. 推送到分支
5. 创建 Pull Request

## 📞 支持

如果遇到任何问题或有疑问，请：
1. 查看上述故障排除部分
2. 查看 GitHub Actions 日志
3. 在仓库中创建 issue
4. 通过邮箱联系作者

---

