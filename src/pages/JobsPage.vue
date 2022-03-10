<template>
  <div class="container-fluid">
    THIS IS WHERE THE JOBS WILL BE....EVENTUALLY
  </div>
</template>


<script>
import { logger } from "../utils/Logger";
import Pop from "../utils/Pop";
export default {
  setup() {
    try {
    } catch (error) {
      logger.error(error);
      Pop.toast(error.message, "error");
    }
    return {};
  },
};
</script>


<style lang="scss" scoped>
</style>