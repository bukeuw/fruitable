<template>
  <div class="container row mx-auto justify-content-center">
    <div v-if="loading">
      <b-spinner></b-spinner>
    </div>
    <div v-else>
      <div class="col mb-4" v-if="fruit.name">
        <b-card
          :title="fruit.name"
          :img-src="'http://localhost:8084' + fruit.image"
          :img-alt="fruit.name"
        >
          <b-card-body>
            <p>{{ fruit.description }}</p>
            <p>{{ fruit.price }}</p>
          </b-card-body>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'FruitDetail',
  data() {
    return {
      fruit: {},
      loading: true,
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.fetchFruit();
    });
  },
  methods: {
    fetchFruit() {
      const fruitId = this.$route.params.id;
      const url = `http://localhost:8084/api/fruits/${fruitId}`;

      this.loading = true;
      axios.get(url)
        .then((fruitJson) => {
          this.fruit = fruitJson.data.data;
          this.loading = false;
        }).catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>
