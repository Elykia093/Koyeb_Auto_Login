https://github.com/Elykia093/Koyeb_Auto_Login
# Koyeb Auto Login

## 项目简介

Koyeb Auto Login 是一个自动化脚本，旨在定期登录 Koyeb 账户，以保持账户的活跃状态。该项目支持两种部署方式：GitHub Actions（推荐）和 Cloudflare Workers。

## 部署方式

### 1. GitHub Actions（推荐）

GitHub Actions 可以定期执行任务，确保 Koyeb 账户保持活跃。

#### **步骤**

1. **Fork 本仓库** 到你的 GitHub 账户。

2. **设置 Secrets**（在仓库的 `Settings` → `Secrets and variables` → `Actions`）：

   | Secret 名称        | 说明                      |
   | ---------------- | ----------------------- |
   | `KOYEB_ACCOUNTS` | 存储 Koyeb 账户信息，格式为 JSON。 |
   | `TG_BOT_TOKEN`   | 你的 Telegram Bot Token。  |
   | `TG_CHAT_ID`     | 你的 Telegram 账号 ID。      |

   **`KOYEB_ACCOUNTS` 格式如下：**
   
   ```json
   [
     {
       "email": "your-email@example.com",
       "password": "your-password"
     },
     {
       "email": "another-email@example.com",
       "password": "another-password"
     }
   ]
   ```

3. **启用 Actions**

   - 在 `Actions` 选项卡中，找到 `Koyeb Auto Login` workflow，点击 `Enable` 以激活 GitHub Actions。

4. **手动运行**

   - 进入 `Actions` → 选择 `Koyeb Auto Login` → `Run workflow` 进行手动测试。

#### **KOYEB\_ACCOUNTS 工作流说明**

GitHub Actions 会在每周日 `00:00 UTC` 运行一次，你可以修改 `.github/workflows/koyeb.yml` 以调整执行频率。

### 2. Cloudflare Workers（可选）

如果你希望更灵活的运行 Koyeb 登录任务，可以使用 Cloudflare Workers。

#### **部署步骤**

1. 在 Cloudflare Workers 创建新的 Worker。
2. 复制 `koyeb.js` 代码粘贴到 Worker 中。
3. 在 Cloudflare KV 中存储 `KOYEB_ACCOUNTS`。
4. 绑定环境变量（`TG_BOT_TOKEN`、`TG_CHAT_ID`）。
5. 设置定时触发器，使 Worker 按计划执行。

## 免责声明

本项目仅用于个人学习和研究，使用者需自行承担使用风险。

