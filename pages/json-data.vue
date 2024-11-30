<template>
  <v-container>
    <h1>Posts from JSON Server</h1>
    <v-row>
      <v-col v-if="!posts.length" cols="12">Loading...</v-col>
      <v-col v-for="post in posts" :key="post.id" cols="12" md="6">
        <v-card>
          <v-card-title>{{ post.title }}</v-card-title>
          <v-card-text>{{ post.body }}</v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      const response = await $axios.get('/posts')
      return { posts: response.data }
    } catch (error) {
      console.error('Error fetching posts:', error)
      return { posts: [] }
    }
  },
}
</script>
