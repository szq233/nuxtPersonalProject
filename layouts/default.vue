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
