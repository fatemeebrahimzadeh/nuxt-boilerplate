<template>
  <v-container>
    <h1>SSR Page</h1>
    <v-row>
      <v-col>
        <p v-if="!data">Loading...</p>
        <div v-else>
          <p><strong>Data from API:</strong></p>
          <ul>
            <li v-for="item in data" :key="item.id">
              {{ item.title }}
            </li>
          </ul>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      const response = await $axios.get(
        'https://jsonplaceholder.typicode.com/posts?_limit=5',
      )
      return { data: response.data }
    } catch (error) {
      console.error('Error fetching data:', error)
      return { data: null }
    }
  },
}
</script>
p
