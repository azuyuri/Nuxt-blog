<template>
  <section id="posts">
    <PostPreview
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      :excerpt="post.previewText"
      :thumbnail-image="post.thumbnailUrl"
      :id="post.id"
      :date="post.date" />
  </section>
</template>

<script>
import PostPreview from "@/components/Blog/PostPreview";
export default {
  components: {
    PostPreview
  },
  asyncData(context) {
    return context.app.$storyapi
      .get('cdn/stories', {
        version: context.isDev ? "draft" : "published",
        starts_with: 'blog/'
    })
    .then(res => {
      // console.log(res);
      return {
        posts: res.data.stories.map(bp => {
          return {
            id:           bp.slug,
            title:        bp.content.title,
            previewText:  bp.content.summary,
            thumbnailUrl: bp.content.thumbnail,
            date:         bp.content.date,
          };
        })
      };
    });
  }
};
</script>
<style scoped>
/* 画面サイズが小さい時縦に配置 */
#posts {
  padding-top: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
/* 画面サイズが大きくなったらまた横に配置 */
@media (min-width: 35rem) {
  #posts {
    flex-direction: row;
  }
}
/* ページ遷移のアニメーション */
.main-content {
  margin-top: 4.5rem;
}
.slide-left-enter {
  transform: translateX(2000px);
  opacity: 0;
}
.slide-left-enter-active {
  transition: all .3s linear;
}
.slide-left-leave-to {
  transform: translateX(-2000px);
  opacity: 0;
}
.slide-left-leave-active {
  transition: all .3s linear;
}

page-enter-active, .page-leave-active {
  transition: opacity .5s;
}
.page-enter, .page-leave-to {
  opacity: 0;
}
</style>
