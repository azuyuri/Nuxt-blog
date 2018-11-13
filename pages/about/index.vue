<template>
  <section
    v-editable="blok"
    id="about-page"
  >
    <h1>{{ title }}</h1>
    <p>{{ content }}</p>
  </section>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories/about', {
      version: context.isDev ? "draft" : "published"
    }).then(res => {
      console.log(res.data)
      return {
        blok: res.data.story.content,
        title: res.data.story.content.title,
        content: res.data.story.content.content
      }
    })
  },
  mounted() {
    this.$storyblok.init();
    this.$storyblok.on("change", () => {
      location.reload(true);
    })
  }
}
</script>

<style>
#about-page {
  width: 80%;
  max-width: 500px;
  margin: auto;
}
#about-page p {
  white-space: pre-line;
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
