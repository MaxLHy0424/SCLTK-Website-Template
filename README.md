# SCLTK & SCLTK-Legacy 下载站 - 部署模板

## 部署指南

在开始下面的步骤前，必须先使用本模板库创建新仓库（推荐创建私有仓库），**不要 Fork 本仓库**。创建之后，先在仓库设置中启用 Actions，再转到 Actions 手动执行一次 `Sync SCLTK-Website`。

### Vercel 部署

1. 注册与登录
  - 访问 [Vercel 官网](https://vercel.com)，点击右上角 “Sign Up”。
  - 支持使用 GitHub、GitLab、Bitbucket 账号一键登录（推荐），也可使用邮箱注册。
  - 若使用 GitHub 登录，请授权 Vercel 访问所需仓库（后续可细化权限）。
  - 登录后，系统会引导你创建团队（个人开发者可直接跳过），进入控制台仪表盘。
2. 导入仓库
  - 在仪表盘中点击 “Add New...” → “Project”。
  - 选择 “Git Repository” 标签页，Vercel 会自动列出你有权限的仓库。
  - 若未显示目标仓库，可点击 “Configure GitHub App” 调整仓库访问权限。
  - 选中仓库后，点击 “Import”。
3. 点击 “Deploy” 按钮，构建成功后，找到 “Production URL”（如 `your-project.vercel.app`），即可访问。
4. 自定义域名（可选）
  - 在项目页面进入 “Settings” → “Domains”。
  - 输入你的自定义域名，点击 “Add”。
  - 根据提示，在你的 DNS 服务商处添加 CNAME 记录，指向 `cname.vercel-dns.com`（或使用 A 记录指向 Vercel 的 IP 地址池）。
  - 若域名由 Vercel 托管（购买或转入），可启用自动 SSL 证书（Let’s Encrypt）并开启 “Force HTTPS”。

### Cloudflare Pages 部署

1. 注册与登录
  - 访问 [Cloudflare 官网](https://dash.cloudflare.com/sign-up)。
  - 在注册页面输入你的邮箱地址和密码。
  - 点击 “Create Account” 按钮。
  - Cloudflare 会向你的邮箱发送一封验证邮件。登录邮箱，点击邮件中的验证链接来完成验证。
  - 注册成功后，点击右上角账户按钮，将语言设置为简体中文。
2. 导入仓库并部署
  - 在左侧侧边栏找到 “计算”，点击 “Workers 和 Pages”。
  - 点击右上角 “创建应用程序”。
  - 点击底部的 “想要部署 Pages？开始使用” 的 “开始使用”。
  - 点击 “导入现有 Git 存储库” 对应的 “开始使用”。
  - 找到并点击你从本仓库创建的新仓库，再点击右下角 “开始设置”。
  - 修改项目名称。
  - 划到下方，找到 “根目录（高级）”，点击 “根目录（高级）”，在 “路径” 下方填入 `public`。
  - 点击 “保存并部署”，等待部署成功。
3. 自定义域名（可选）
  - 转到 “Workers 和 Pages”，找到刚刚创建的实例，点击进入实例设置。
  - 点击上方 “自定义域”，点击 “设置自定义域”，输入你的自定义域名，按照提示设置。

### PinMe 部署

1. 注册与登录
  - 访问 [PinMe 官网](https://pinme.eth.limo)，点击右上角 “登录”，根据提示登录即可。
2. 获取 AppKey
  - 访问 [Profile 页面](https://pinme.eth.limo/#/profile)，找到 AppKey，点击复制。**请妥善保管 AppKey**。
3. 设置环境变量
  - 转到仓库设置，找到 “Secrets and variables”，点击 “Actions”。
  - 点击 “New repository secret”。
  - 新增 `PINME_APPKEY`，值为你的 AppKey。
4. 修改 Workflow 文件。
  - 转到 `.github/workflows/deploy-to-pinme.yaml`。
  - 取消 `on:` 下方 `push` 块的注释。
  - 找到 `default_domain`，修改后方内容为你想要的默认域名**前缀**。默认为当前仓库名。**注意：域名前缀字符数应控制在 3 ~ 20 内。后方内容要带引号。** 示例：`default_domain: "scltk"`。
  - 尝试手动运行一次。所得的域名为 `域名前缀.pinme.dev`。注意查看 Actions 的 “Deploy to PinMe” 下的输出，如果出现 `Error: fail` 字样，请检查域名前缀是否被占用或字符数是否满足要求。

<!-- todo：添加 Pinata 部署指南 -->
