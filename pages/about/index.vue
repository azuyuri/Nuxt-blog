<template>
  <section id="about-page">
    <h1>{{ title }}</h1>
    <p>{{ content }}</p>
  </section>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories/about', {
      version: 'draft'
    }).then(res => {
      return {
        title: res.data.content.title,
        content: res.data.content.content
      }
    })
  }
}
</script>
