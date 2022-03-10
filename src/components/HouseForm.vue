<template>
  <form>
    <div class="form-group">
      <label for="bedrooms" class="">Bedrooms</label>
      <input
        v-model="editable.bedrooms"
        type="number"
        name="bedrooms"
        id="bedrooms"
        class="form-control"
        placeholder="Bedrooms"
        required
      />
    </div>
    <div class="form-group">
      <label for="bathrooms" class="">Bathrooms</label>
      <input
        v-model="editable.bathrooms"
        type="number"
        name="bathrooms"
        id="bathrooms"
        class="form-control"
        placeholder="Bathrooms"
        required
      />
    </div>
    <div class="form-group">
      <label for="year" class="">Built Year</label>
      <input
        v-model="editable.year"
        type="number"
        name="year"
        id="year"
        class="form-control"
        placeholder="Year"
        required
      />
    </div>
    <div class="form-group">
      <label for="price">Price:</label>
      <input
        v-model="editable.price"
        type="number"
        name="price"
        id="price"
        class="form-control"
        min="0"
        max="999999999"
        placeholder="Price"
        required
      />
    </div>
    <div class="form-group">
      <label for="description">Description:</label>
      <input
        v-model="editable.description"
        type="text"
        name="description"
        id="description"
        class="form-control"
        placeholder="Description"
        required
      />
    </div>
    <div class="form-group">
      <label for="imgUrl">IMG</label>
      <input
        v-model="editable.imgUrl"
        type="url"
        name="imgUrl"
        id="imgUrl"
        class="form-control"
        placeholder="Photo"
        required
      />
    </div>
    <div class="d-flex justify-content-between my-3">
      <button
        type="button"
        data-bs-dismiss="modal"
        aria-label="Close"
        class="btn text-dark lighten-20 text-uppercase selectable"
      >
        <b> cancel </b>
      </button>
      <button
        v-if="!houseData.id"
        @click="createHouse"
        type="button"
        class="btn btn-success text-dark text-uppercase selectable"
      >
        <b> Create House </b>
      </button>
      <button
        v-else
        @click="editHouse"
        type="button"
        class="btn btn-info text-warning text-uppercase selectable"
      >
        <b> Edit House </b>
      </button>
    </div>
  </form>
</template>


<script>
import { ref, watchEffect } from "@vue/runtime-core";
import { useRouter } from "vue-router";
import { logger } from "../utils/Logger";
import { housesService } from "../services/HousesService";
import { Modal } from "bootstrap";
import Pop from "../utils/Pop";
export default {
  props: {
    houseData: {
      type: Object,
      required: false,
      default: {},
    },
  },
  setup(props) {
    const editable = ref({});
    const router = useRouter();
    watchEffect(() => {
      logger.log("change occurred, re-run watch effect");
      editable.value = props.houseData;
    });
    return {
      editable,
      async createHouse() {
        try {
          let newHouse = await housesService.create(editable.value);
          editable.value = {};
          Modal.getOrCreateInstance(
            document.getElementById("form-modal")
          ).hide();
          router.push({ name: "HouseDetails", params: { id: newHouse.id } });
        } catch (error) {
          logger.error(error);
          Pop.toast(error.message, "error");
        }
      },
    };
  },
};
</script>


<style lang="scss" scoped>
</style>