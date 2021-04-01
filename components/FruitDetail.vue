<template>
  <v-col :cols="4">
    <v-card :loading="$fetchState.pending">
      <v-img :src="`http://localhost:8084${fruit.image}`"> </v-img>
      <v-card-text>
        {{ fruit.name }}
      </v-card-text>
      <v-card-text>
        {{ fruit.price }}
      </v-card-text>
    </v-card>
  </v-col>
</template>

<script>
export default {
  fetch() {
    this.fetchFruits()
  },
  fetchOnServer: false,
  data() {
    return {
      fruit: [],
      baseUrl: 'http://localhost:8084/api',
    }
  },
  methods: {
    fetchFruits() {
      const fruitId = this.$route.params.id
      const url = `${this.baseUrl}/fruits/${fruitId}`
      this.$axios
        .$get(url)
        .then((fruitsJson) => {
          this.fruit = fruitsJson.data
        })
        .catch((err) => {
          // eslint-disable-next-line
          console.error(err)
        })
    },
  },
}
</script>
