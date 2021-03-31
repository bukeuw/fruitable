<template>
  <div class="fruits">
    <FruitDetail></FruitDetail>
  </div>
</template>

<script>
// @ is an alias to /src
import FruitDetail from '@/components/FruitDetail.vue';

export default {
  name: 'Detail',
  components: {
    FruitDetail,
  },
};
</script>
