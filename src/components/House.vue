<template>
  <router-link :to="{ name: 'HouseDetails', params: { id: house.id } }">
    <div class="row p-2 bg-light shadow rounded selectable">
      <div class="col-12">
        <img :src="house.imgUrl" alt="" class="img-fluid" />
      </div>
      <h3 class="text-center col-12 p-1">
        <div>{{ house.bedrooms }} | Bed</div>
        <div>{{ house.bathrooms }} | Bath</div>
        <div>Built | {{ house.year }}</div>
      </h3>
    </div>
  </router-link>
</template>


<script>
export default {
  props: {
    house: {
      type: Object,
      required: true,
    },
  },
  setup() {
    return {};
  },
};
</script>


<style lang="scss" scoped>
.house {
  transition: all 0.2s ease;
}
.car:hover {
  transform: scale(1.03);
}
</style>