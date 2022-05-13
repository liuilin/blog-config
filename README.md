> 如果是首次搭建 Hexo，请先看文章《GitHub+Hexo 搭建个人网站》
## 恢复环境

```bash
git clone https://github.com/liuilin/blog-content-config.git
npm install # 安装依赖的 module 模块
```

### Hexo 相关执行命令

```bash
hexo clean
hexo n 'xxx'(new 新建博客在 source\_posts 文件目录下)
hexo g(enerate 生成文档对应的 html 链接)
hexo s(本地访问预览 localhost:4000)
hexo d(eploy 部署发布到 GitHub，具体发布路径配置在 _config.yml 下对应的 deploy 配置)
```