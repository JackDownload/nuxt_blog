<template>
  <section class="slug">
    <h1 class="slug_title">{{ post.fields.title }}</h1>
    <p class="slug_date">
      {{ post.fields.publishedAt | datetime }}
    </p>
    <!-- eslint-disable-next-line vue/no-v-html -->
    <div v-html="$md.render(post.fields.body)"></div>
  </section>
</template>

<script>
import createClient from '~/plugins/contentful'

const client = createClient()
export default {
  transition: 'slide-left',
  filters: {
    datetime: function(value) {
      const date = new Date(value)
      return date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
    },
  },
  asyncData({ env, params }) {
    return client
      .getEntries({
        content_type: env.CTF_BLOG_POST_TYPE_ID,
        'fields.slug': params.slug,
        order: '-sys.createdAt',
      })
      .then(entries => {
        return {
          post: entries.items[0],
        }
      })
      .catch(console.error)
  },
}
</script>

<style scoped>
.slug {
  max-width: 800px;
  margin: 0 auto;
}
.slug_title {
  font-size: 2rem;
  font-weight: bolder;
}
.slug_date {
  font-size: 1rem;
  color: rgb(57, 72, 85);
  text-align: right;
}
</style>
