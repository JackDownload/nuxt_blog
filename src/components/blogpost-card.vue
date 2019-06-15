<template>
  <v-layout>
    <v-flex xs12 sm6 offset-sm3>
      <template v-for="post in posts">
        <v-card :key="post.sys.id" flat>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{ post.fields.title }}</h3>
            </div>
          </v-card-title>
          <v-card-text primary-title>
            {{ post.fields.publishedAt | datetime }}
          </v-card-text>
          <v-card-actions>
            <v-btn
              flat
              color="blue"
              :to="{ name: 'blog-slug', params: { slug: slug } }"
            >
              read more...
            </v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  filters: {
    datetime: function(value) {
      const date = new Date(value)
      return date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
    },
  },
  props: {
    posts: {
      type: Array,
      default: function() {
        return []
      },
    },
  },
}
</script>
