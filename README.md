# 每日科技资讯推送

每天早上自动抓取科技资讯并推送到微信的工作流。

## 功能

- 自动抓取过去24小时的科技资讯
- 支持多个RSS源：36氪、虎嗅、爱范儿、TechCrunch
- 每天早上7点自动运行
- 通过Server酱推送到微信

## 快速部署

### 1. 配置 Server酱

1. 访问 [Server酱官网](https://sct.ftqq.com/) 注册账号
2. 获取你的 SendKey
3. 进入仓库 → **Settings** → **Secrets and variables** → **Actions**
4. 新建 Secret：
   - Name: `SEND_KEY`
   - Secret: 你的Server酱SendKey

### 2. 手动测试

1. 进入仓库的 **Actions** 页面
2. 选择 **"每日科技资讯推送"** 工作流
3. 点击 **"Run workflow"** 手动触发

### 3. 查看运行日志

在 Actions 页面点击具体的运行记录，可以查看执行日志和推送结果。

## 文件说明

```
.
├── fetch_news.py              # Python 抓取脚本
├── requirements.txt           # Python 依赖
└── .github/workflows/
    └── daily_tech_news.yml   # GitHub Actions 工作流
```

## 定时任务

工作流每天 **北京时间早上7点** 自动运行。

如需调整时间，修改 `.github/workflows/daily_tech_news.yml` 中的 cron 表达式：

```yaml
schedule:
  # 每天7点运行 (UTC 23:00 = 北京时间 7:00)
  - cron: '0 23 * * *'
```

如需了解 cron 表达式格式，请参考 [GitHub Actions 文档](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule)。

## 本地运行

```bash
# 安装依赖
pip install -r requirements.txt

# 设置环境变量
export SEND_KEY="你的SendKey"

# 运行脚本
python fetch_news.py
```

## RSS 源

- 36氪: <https://www.36kr.com/feed/>
- 虎嗅网: <https://www.huxiu.com/rss.xml>
- 爱范儿: <https://www.ifanr.com/feed/>
- TechCrunch: <https://techcrunch.com/feed/>
