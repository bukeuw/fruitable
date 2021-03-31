<template>
  <div class="container row mx-auto">
    <div
      v-for="fruit in fruits"
      :key="fruit.id"
       class="col-4 mb-4"
    >
      <router-link :to="'/fruits/' + fruit.id">
        <b-card
          :title="fruit.name"
          :img-src="'http://localhost:8084' + fruit.image"
          :img-alt="fruit.name"
        >
          <b-card-body>
            <p>{{ fruit.price }}</p>
          </b-card-body>
        </b-card>
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'FruitList',
  data() {
    return {
      fruits: [],
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.fetchFruit();
    });
  },
  methods: {
    fetchFruit() {
      const url = 'http://localhost:8084/api/fruits';

      axios.get(url)
        .then((fruitsJson) => {
          this.fruits = fruitsJson.data.data;
        }).catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>
