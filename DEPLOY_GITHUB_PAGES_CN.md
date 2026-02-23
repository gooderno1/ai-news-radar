# AI 日报看板（GitHub Actions + Pages）部署说明

## 已完成（仓库内）

- 已有定时更新工作流：`.github/workflows/update-news.yml`
  - 每 30 分钟抓取一次并更新 `data/*`
- 已新增 Pages 发布工作流：`.github/workflows/deploy-pages.yml`
  - 当 `index.html` / `assets/*` / `data/*` 变化时自动发布

## 你只需做的 3 件事（一次性）

1. 把代码推到你自己的 GitHub 仓库（默认分支 main/master 都可）。
2. 在仓库 Settings → Pages：
   - Build and deployment 选择 **GitHub Actions**。
3. 在仓库 Settings → Actions → General：
   - Workflow permissions 选择 **Read and write permissions**。

## 可选配置（推荐）

### 私有 RSS OPML

在仓库 Settings → Secrets and variables → Actions 新增：

- Name: `FOLLOW_OPML_B64`
- Value: 你的 `feeds/follow.opml` 文件内容做 base64 后的字符串

生成方式（Linux/WSL/macOS）：

```bash
base64 -w 0 feeds/follow.opml
```

> 不要把真实 OPML 文件直接提交到仓库。

## 验证上线

1. 打开 Actions，手动运行一次 `Update AI News Snapshot`。
2. 再看 `Deploy AI News Board to GitHub Pages` 是否成功。
3. 访问：

- `https://<你的用户名>.github.io/<仓库名>/`

若是用户/组织主页仓库（`<用户名>.github.io`），则直接访问根域名。

## 结果形态

- 一个每日可浏览的网页看板（静态页面）
- 数据自动刷新（默认每 30 分钟）
- 无需本地常驻脚本

## 之后可升级

- 自定义域名（CNAME）
- 接入 VPS（Nginx + cron）做内网/鉴权版
- 增加“昨日/7日趋势”“订阅源健康告警”
