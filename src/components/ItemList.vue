<template>
  <div>
    <div class="container">
      <table class="table">
        <thead class="bg-dark text-light">
          <tr>
            <th scope="col">
              <span class="mr-1">Name</span>
              <i @click="$emit('sortItems')" class="fas fa-sort-up"></i>
            </th>
            <th scope="col">Code</th>
            <th scope="col">Action</th>
          </tr>
        </thead>
            <paginate tag="tbody" name='getItems' :list="getItem" :per="limit" :key="getItem ? getItem.length : 0">
              <tr v-for="item in paginated('getItems')" :key="item.id">
                <td>
                  <input v-if="item.isChange" v-model.trim="item.name" type="text" class="form-control" :class="!item.name.length ? 'form-invalid' : ''">
                  <span v-else>{{ item.name }}</span>
                  <div v-if="!item.name.length" class="invalid-feedback d-block">
                    This field is required
                  </div>
                </td>
                <td>{{ item.id }}</td>
                <td>
                  <button @click="$emit('deleteItem', item)" type="button" class="btn btn-danger mr-3">
                    <i class="far fa-times-circle"></i>
                  </button>
                  <button :disabled="!item.name.length" @click="item.isChange = !item.isChange" type="button" class="btn btn-success">
                    <i class="far fa-edit"></i>
                  </button>
                </td>
              </tr>
            </paginate>
      </table>
      <paginate-links v-if="getItem.length" class="list-unstyled d-flex justify-content-center" for="getItems" :limit="5" :show-step-links="true"></paginate-links>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import VuePaginate from 'vue-paginate'
Vue.use(VuePaginate)

export default Vue.extend({
  name: 'ItemList',
  props: {
    arr: {
      type: Array,
      default: () => []
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
  data() {
    return {
      paginate: ['getItems'] as string[]
    }
  },
  computed: {
    getItem () {
      return this.arr.filter((item: any) => {
        return item.name.toLowerCase().includes(this.itemName.toLowerCase())
      })
    }
  }
});
</script>

<style>

.number {
  margin: 0 10px;
}

.paginate-links li a {
  padding: .5rem .75rem;
  line-height: 1.25;
  color: #007bff;
  background-color: #fff;
  border: 1px solid #dee2e6;
  cursor: pointer;
}

.paginate-links li a:hover {
  background-color: #e9ecef;
}

</style>
