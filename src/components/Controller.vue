<template>
  <div>
    <div class="container mb-5">
      <div class="row justify-content-around align-items-center">
        <div class="col-md-4 d-flex">
          <button @click="$emit('emitModal', true)" type="button" class="btn btn-danger mr-3">
            <i class="fas fa-plus-circle"></i>
          </button>
          <div class="input-group">
            <input
              type="text"
              class="form-control"
              aria-label="Recipient's username"
              aria-describedby="button-addon2"
              v-model.trim="searchItemName"
              @input="$emit('update:itemName', searchItemName)"
            />
            <div class="input-group-append">
              <button class="btn btn-outline-success" type="button" id="button-addon2">
                <i class="fas fa-search"></i>
              </button>
            </div>
          </div>
        </div>
        <div class="col-md-2 text-center">
          <h1>{{title}}</h1>
        </div>
        <div class="col-md-2">
          <select v-model.number="newLimit" @change="$emit('update:limit', newLimit)" class="form-control" id="exampleFormControlSelect1">
            <option>5</option>
            <option>10</option>
            <option>15</option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: 'Controller',
  props: {
    title: {
      type: String,
      default: 'Users'
    },
    itemName: {
      type: String,
      default: ''
    },
    limit: {
      type: Number,
      default: 5
    }
  },
  data () {
    return {
      newLimit: 5 as number,
      searchItemName: '' as string
    }
  }
});
</script>

<style scoped>
</style>
