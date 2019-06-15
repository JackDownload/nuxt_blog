<template>
  <blogpost-card :posts="posts" />
</template>

<script>
import BlogpostCard from '~/components/blogpost-card.vue'
import createClient from '~/plugins/contentful'

const client = createClient()
export default {
  transition: 'slide-left',
  components: {
    BlogpostCard,
  },
  asyncData({ env, params }) {
    return client
      .getEntries({
        content_type: env.CTF_BLOG_POST_TYPE_ID,
        order: '-fields.publishedAt',
      })
      .then(entries => {
        return {
          posts: entries.items,
        }
      })
      .catch(console.error)
  },
}
</script>

<style scoped>
.index {
  display: flex;
  flex-wrap: wrap;
}
</style>
