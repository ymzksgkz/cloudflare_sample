<template>
  <div>
    <span>記事一覧</span>
    <div class="article" v-for="article in contents">
      <NuxtLink :to="`/articles/${article.id}`" >
        <span>{{ article.title }}</span>
      </NuxtLink>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ArticleList',
  data() {
    return {
      contents: {}
    }
  }, async created() {
    const { data: { contents } } = await axios.get(
        `https://cms-practice.microcms.io/api/v1/news`,
        {
          // TODO 環境変数にしたほうがよいけど一旦いい。
          headers: {'X-MICROCMS-API-KEY': 'a85dd8764e99460e92d2bdf73906732c1a56'}
        }
    )
    this.contents = contents
  }
}
</script>
<style lang="css">
.article {
  margin: 10px;
}

a {
  text-decoration: none;
}
</style>