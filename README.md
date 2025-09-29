# 自动跑步步数提交脚本

这是一个自动提交跑步步数的脚本，支持多账号，可以通过GitHub Actions实现每天定时自动执行。

## 功能特点

- 🏃‍♂️ 支持多账号同时提交
- ⏰ 根据时间段智能生成步数
- 🔒 支持环境变量配置，保护账号安全
- 🤖 GitHub Actions自动化执行
- 📊 详细的执行日志

## 步数生成规则

脚本会根据当前时间智能生成步数：

- **8点**: 6000-10000步
- **12点**: 8000-14000步  
- **16点**: 10000-18000步
- **20点**: 12000-22000步
- **22点**: 15000-24000步
- **其他时间**: 默认24465步

## 本地运行

1. 安装依赖：
```bash
pip install -r requirements.txt
```

2. 直接运行：
```bash
python auto_zeep.py
```

## GitHub Actions自动化设置

### 1. 创建GitHub仓库

将代码推送到GitHub仓库。

### 2. 配置Secrets

在GitHub仓库中设置以下Secrets（Settings → Secrets and variables → Actions）：

- `ACCOUNT1_USERNAME`: 第一个账号的用户名
- `ACCOUNT1_PASSWORD`: 第一个账号的密码
- `ACCOUNT2_USERNAME`: 第二个账号的用户名  
- `ACCOUNT2_PASSWORD`: 第二个账号的密码
- `ACCOUNT3_USERNAME`: 第三个账号的用户名（可选）
- `ACCOUNT3_PASSWORD`: 第三个账号的密码（可选）
- ...（最多支持5个账号）

### 3. 执行时间设置

默认设置为每天北京时间早上8点执行。如需修改时间，编辑 `.github/workflows/auto-run.yml` 文件中的cron表达式：

```yaml
schedule:
  - cron: '0 0 * * *'  # UTC时间0点，即北京时间8点
```

### 4. 手动触发

你也可以在GitHub仓库的Actions页面手动触发执行。

## 文件说明

- `auto_zeep.py`: 主脚本文件
- `requirements.txt`: Python依赖包
- `.github/workflows/auto-run.yml`: GitHub Actions工作流配置
- `README.md`: 说明文档

## 注意事项

1. **账号安全**: 请使用GitHub Secrets存储账号密码，不要直接写在代码中
2. **执行频率**: 避免过于频繁的提交，建议每天执行一次
3. **网络环境**: 确保GitHub Actions能够正常访问目标API
4. **日志监控**: 定期检查执行日志，确保脚本正常运行

## 故障排除

如果执行失败，请检查：

1. GitHub Secrets是否正确配置
2. 网络连接是否正常
3. 账号密码是否正确
4. API接口是否有变化

## 许可证

本项目仅供学习和研究使用，请遵守相关服务条款。
