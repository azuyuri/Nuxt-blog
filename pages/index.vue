<template>
  <section class="container">
    <nuxt-link
      v-for="post in posts"
      :key="post.id"
      to="post.id">
      <article class="post-preview">
        <div
          :style="{backgroundImage: post.thumbnailUrl}"
          class="post-preview-thumbnail"/>
        <div class="post-preview-content">
          <h1>{{ post.title }}</h1>
          <p>{{ post.previewText }}</p>
        </div>
      </article>
    </nuxt-link>
  </section>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        {
          title: 'A New Beginning',
          previewText: 'This will be awesome, don\'t miss it! ',
          thumbnailUrl: 'http://www.healthyfood.co.uk/wp-content/uploads/2015/01/Cherry-tomato-bocc-olive-basil-pasta.jpg',
          id: 'a-new-beginning'
        },
         {
          title: 'A Second Beginning',
          previewText: 'This will be awesome, don\'t miss it! ',
          thumbnailUrl: 'http://www.healthyfood.co.uk/wp-content/uploads/2015/01/Cherry-tomato-bocc-olive-basil-pasta.jpg',
          id: 'a-second-beginning'
        }
      ]
    }
  }
}
</script>

<style>

</style>
