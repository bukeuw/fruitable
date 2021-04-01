<template>
  <v-col :cols="4">
    <v-card
      v-for="fruit in fruits"
      :key="fruit.id"
      :loading="$fetchState.pending"
    >
      <router-link :to="`/fruits/${fruit.id}`">
        <v-img :src="`http://localhost:8084${fruit.image}`"> </v-img>
      </router-link>
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
      fruits: [],
      baseUrl: 'http://localhost:8084/api',
    }
  },
  methods: {
    fetchFruits() {
      const url = `${this.baseUrl}/fruits`
      this.$axios
        .$get(url)
        .then((fruitsJson) => {
          this.fruits = fruitsJson.data
        })
        .catch((err) => {
          // eslint-disable-next-line
          console.error(err)
        })
    },
  },
}
</script>
