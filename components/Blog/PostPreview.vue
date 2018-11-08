<template>
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
</template>
