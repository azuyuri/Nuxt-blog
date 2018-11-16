<template>
  <div
    v-editable="blok"
    id="post">
    <div
      :style="{backgroundImage: 'url(' + image + ')'}"
      class="post-thumbnail"/>
    <section
      class="post-content"
    >
      <h1>{{ title }}</h1>
      <span
        class="date">
        {{ date }}
      </span>
      <p>{{ content }}</p>
      <a
        :href="link.url"
        class="links">
        {{ link.url }}
      </a>
    </section>
  </div>
</template>

<script>
  export default {
    head () {
    return {
      link: [
        {
          rel: 'stylesheet',
          href: 'https://use.fontawesome.com/releases/v5.5.0/css/all.css',
          href: 'https://use.fontawesome.com/releases/v5.5.0/css/solid.css'
          }
        ]
      }
    },
    asyncData(context) {
    return context.app.$storyapi
      .get('cdn/stories/blog/' + context.params.postId, {
        version: process.env.NODE_ENV == 'production' ? 'published' : 'draft'
      })
      .then(res => {
        return {
          blok: res.data.story.content,
          image: res.data.story.content.thumbnail,
          title: res.data.story.content.title,
          content: res.data.story.content.content,
          date: res.data.story.content.date,
          link: res.data.story.content.link,
        };
      });
    },
    mounted() {
      this.$storyblok.init();
      this.$storyblok.on("change", () => {
        location.reload(true);
      });
    },
  }
</script>

<style>
.post-thumbnail {
  width: 100%;
  height: 300px;
  background-size: cover;
  background-position: 50% 30%;
}
.post-content {
  width: 80%;
  max-width: 500px;
  margin: auto;
}
.post-content p {
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

/* date */
.date {
  color: #738A8D;
  font-size: 0.93em;
}

.date:before {
    font-family: "Font Awesome 5 Free";
    content: '\f073';
    color: #738A8D;
    margin-right: .4em;
}

/* link */
.links {
    position: relative;
    text-decoration: none;
    color: #738A8D;
}
a:hover {
    color: #000;
    transition: 1.0s;
}

.links:before {
    font-family: "Font Awesome 5 Free";
    content: '\f0c1';
    position: absolute;
    left: -1.2em;
    top: 2px;
    color: #000;
    margin-right: .4em;
}

</style>
