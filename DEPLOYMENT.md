# Typecho Vercel + Supabase 部署指南

## 概述

本项目配置为在Vercel上运行Typecho博客系统，使用Supabase作为PostgreSQL数据库。

## 当前配置

### Vercel配置
- 使用 `vercel-php@0.7.4` 运行时
- 所有请求路由到 `api/index.php`
- 支持PHP 7.4+

### 数据库配置
- 使用Supabase PostgreSQL数据库
- 采用PDO PostgreSQL驱动
- 支持SSL连接
- 使用环境变量管理敏感信息

## 部署步骤

### 1. 准备Supabase数据库

1. 在Supabase控制台创建新项目
2. 获取数据库连接信息：
   - 主机地址
   - 端口号
   - 用户名
   - 密码
   - 数据库名

### 2. 初始化数据库表

在Supabase的SQL编辑器中执行 `install/Pgsql.sql` 文件中的SQL语句，创建Typecho所需的表结构。

### 3. 配置Vercel环境变量

在Vercel项目设置中添加以下环境变量：

```
DB_HOST=your-supabase-host
DB_PORT=6543
DB_USER=your-supabase-user
DB_PASSWORD=your-supabase-password
DB_NAME=postgres
```

### 4. 部署到Vercel

```bash
# 安装Vercel CLI
npm i -g vercel

# 登录Vercel
vercel login

# 部署项目
vercel --prod
```

### 5. 完成安装

部署完成后，访问您的Vercel域名，Typecho会自动跳转到安装页面。按照安装向导完成配置。

## 注意事项

### 文件上传限制
Vercel是无服务器环境，不支持传统的文件上传。如果需要文件上传功能，建议：

1. 使用外部存储服务（如AWS S3、Cloudinary）
2. 开发插件来处理文件上传到外部存储

### 性能优化
- 启用Vercel的缓存功能
- 考虑使用CDN加速静态资源
- 优化数据库查询

### 安全建议
- 定期更新数据库密码
- 启用Supabase的行级安全策略
- 监控访问日志
- 使用环境变量存储敏感信息

## 故障排除

### 数据库连接问题
1. 检查环境变量是否正确设置
2. 确认Supabase连接字符串格式
3. 验证SSL连接设置
4. 检查PDO PostgreSQL驱动是否可用

### 部署失败
1. 检查Vercel日志
2. 确认PHP版本兼容性
3. 验证文件权限设置

## 支持

如遇到问题，请检查：
- Vercel部署日志
- Supabase数据库连接状态
- Typecho错误日志 