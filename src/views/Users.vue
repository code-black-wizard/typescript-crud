<template>
  <div>
    <Controller @emitModal="emitModal" :itemName="itemName" :limit="limit" @update:itemName="itemName = $event" @update:limit="limit = $event" :title="title" />
    <Modal v-show="showModal" @createItem="createItem" @emitModal="emitModal" :title="titleModal" />
    <ItemList :arr="users" :itemName="itemName" :limit="limit" @deleteItem="deleteItem" @sortItems="sortItems" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Controller from '@/components/Controller.vue';
import Modal from '@/components/UI/Modal.vue';
import ItemList from '@/components/ItemList.vue';
import { Item } from '../types/index';

export default Vue.extend({
  name: 'Users',
  components: {
    Controller,
    Modal,
    ItemList
  },
  data () {
    return {
      title: 'Users' as string,
      titleModal: 'User' as string,
      showModal: false as boolean,
      users: [] as Item[],
      itemName: '' as string,
      limit: 5 as number
    }
  },
  methods: {
    emitModal (data: boolean) {
      this.showModal = data
    },
    createItem (data: string) {
      this.users.push({
        name: data,
        id: Math.random(),
        isChange: false
      })
    },
    deleteItem (item: Item) {
      this.users.splice(this.users.indexOf(item), 1)
    },
    sortItems () {
      return this.users.sort((a,b) => {
        if (a.name < b.name) {
          return -1
        } else {
          return 1
        }
        return 0
      })
    }
  },
  watch: {
    users: {
      deep: true,
      handler() {
         localStorage.setItem('users', JSON.stringify(this.users));
      }
    }
  },
  created() {
    if (localStorage.getItem('users')) {
      this.users = JSON.parse(localStorage.getItem('users'));
    }
  }
})
</script>
