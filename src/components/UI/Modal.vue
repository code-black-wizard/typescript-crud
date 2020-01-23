<template>
  <div>
    <div class="modal d-block" tabindex="-1" role="dialog">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header border-0">
            <h5 class="modal-title">Create {{ title }}</h5>
            <button @click="$emit('emitModal', false)" type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <form @submit.prevent="createItem">
            <div class="modal-body">
              <input v-model.trim="name" class="form-control" :class="error ? 'form-invalid' : ''" type="text">
              <div v-if="error" class="invalid-feedback d-block">
                This field is required
              </div>
            </div>
            <div class="modal-footer border-0">
              <button type="submit" class="btn btn-primary">Create</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "Modal",
  props: {
    title: {
      type: String,
      default: 'Users'
    }
  },
  data() {
    return {
      name: '' as string,
      error: false as boolean
    };
  },
  methods: {
    createItem () {
      if (this.name.length) {
        this.$emit('createItem', this.name)
        this.$emit('emitModal', false)
        this.name = ''
        this.error = false as boolean
      } else {
        this.error = true as boolean
      }
    }
  }
});
</script>

<style>

.modal {
  background-color: rgba(0,0,0,0.4);
}

.form-invalid {
  border-color: #dc3545;
}

</style>
