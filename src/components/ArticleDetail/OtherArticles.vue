<template>
  <div class="article">
    <div class="article-cover">
      <img :src="require('@/assets/images/grass.jpg')" alt="">
    </div>
    <div class="info">
      <router-link class = "article-title":to="{ path: '/view', query: { id: this.article.articleId }}" @click.native="flushCom">{{ ArticleTitle }}</router-link>
      <div class="article-time">{{ formatTime }}</div>
      <div class="article-content">{{ brief }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Article',
  // 接收父组件传来的 article 对象
  props: {
    article: Object
  },
  // 计算属性
  computed: {
    // 对时间进行格式化
    formatTime: function() {
      if (this.article) {
        return this.article.releaseDate.toString().substr(0,10)
      }
      return '';
    },
    // 截取文章内容的前 35 个字，并加上省略号
    brief: function() {
      return this.article.abstractContent
    },
    ArticleTitle: function () {
      return this.article.title
    }
  },
  methods: {
    flushCom(){
      this.$router.go(0)
    }
  }

}

</script>

<style lang="scss" scoped>
.article {
  width: 400px;
  display: flex;
  padding: 10px 0;
  border-bottom: 1px solid #dbdbdb;
  &:last-child {
    border: none;
  }
  .article-title {
    font-size: 20px;
    font-weight: 500;
    color: #000000;
    text-align: justify;
  }
  .article-cover {
    flex: none;
    width: 120px;
    margin-right: 10px;
    > img {
      width: 100%;
    }
  }
  .article-content, .article-time {
    font-size: 14px;
  }
  .article-time {
    margin: 10px 0;
    color: #c5c5c5;
  }
}
</style>