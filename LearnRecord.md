# 使用手记

## 1、脚手架安装项目

1. `yarn create nuxt-app <项目名>` 或者 `create-nuxt-app <项目名>`

2. 构建项目的相关选项选择:
   - 主要是模式选择Universal, ssr渲染;
   - 选择element ui插件;
   - 还有一个多出来的server选项，选择node-server, 然后完成项目创建，提交一下初始化项目git记录。

3. 安装sass功能实现依赖:
   - 首先查看一下本地环境node的版本对应版本，下载node-sass依赖，以下是node-sass的文档内容中的版本关系:
     NodeJS |Supported node-sass version|Node Module
     -------|---------------------------|-----------
     Node 17|7.0+                       |102
     Node 16|6.0+                       |93
     Node 15|5.0+, <7.0                 |88
     Node 14|4.14+                      |83
     Node 13|4.13+, <5.0                |79
     Node 12|4.12+                      |72
     Node 11|4.10+, <5.0                |67
     Node 10|4.9+, <6.0                 |64
     Node 8 |4.5.3+, <5.0               |57
     Node <8|<5.0                       |<57
   - 我这边node版本是`v14.3.0`只需要安装`^4.14.0`版本的node-sass就可以了, `yarn add -D node-sass@4.14.1`, 可以在包名后只跟一个@符号，这样会列出可选版本列表。
   - 网上搜索一下与当前版本node-sass兼容的sass-loader,我这边是安装`^10.1.1`, `yarn add -D sass-loader@10.1.1`。
   - 安装"@nuxtjs/style-resources": "^1.2.1", `yarn add @nuxtjs/style-resources`,这边也注意一下版本,安装这个插件是为了是sass支持nuxt.config.js中配置Global CSS。

## 2、好好阅读Nuxt官方文档

- 这边需要参考**Nuxt官网**的目录结构、配置、路由等文档说明( [Nuxt文档](https://www.nuxtjs.cn/guide/directory-structure) )。

## 3、开始项目

### 1、路由说明

    在pages文件夹中添加的文件夹会自动被读取并生成路由表。
    使用<nuxt-link :to="/">首页</nuxt-link>可以实现点击路由跳转

### 2、视图

    配置布局，默认布局的源码是:
    <template>
      <nuxt />
    </template>

    <nuxt />为路由渲染位置
    ---------------------------------------
    可以自定义布局, 比如在layouts文件夹中创建一个vue文件layouts/about.vue:
    <template>
      <div>
        <div>这里是关于</div>
        <nuxt />
      </div>
    </template>
    在页面中使用:
    <template>
      <!-- Your template -->
    </template>
    <script>
      export default {
        layout: 'about'
        // page component definitions
      }
    </script>
    ---------------------------------------
    配置默认视图, 需要在layouts文件夹中创建default.vue, 如下配置后可以生成一个切换路由的导航栏:
    <template>
      <div>
        <div>
          <template v-for="(item, i) in navigation">
            <nuxt-link :key="i" :to="item.path">{{item.title}}</nuxt-link>
            >>
          </template>
        </div>
        <nuxt />
      </div>
    </template>

    <script>
    export default {
      data() {
        return {
          navigation: [
            { title: '首页', path: '/' },
            { title: '关于', path: '/about' },
            { title: '服务支持', path: '/support' },
          ]
        }
      }
    }
    </script>
