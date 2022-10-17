<template>
  <div>
    <span>記事一覧</span>
    <div class="article" v-for="article in contents" :key="article.id">
      <NuxtLink :to="`/articles/${article.id}`" >
        <span>{{ article.title }}</span>
      </NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ArticleList',
  async asyncData(ctx) {
    const { contents } = await ctx.$axios.$get(
        `https://cms-practice.microcms.io/api/v1/news`,
        {
          // TODO 環境変数にしたほうがよいけど一旦いい。
          headers: {'X-MICROCMS-API-KEY': 'a85dd8764e99460e92d2bdf73906732c1a56'}
        }
    )
    return { contents }
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