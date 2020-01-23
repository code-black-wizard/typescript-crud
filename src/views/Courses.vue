<template>
  <div>
    <Controller @emitModal="emitModal" :itemName="itemName" :limit="limit" @update:itemName="itemName = $event" @update:limit="limit = $event" :title="title" />
    <Modal v-show="showModal" @createItem="createItem" @emitModal="emitModal" :title="titleModal" />
    <ItemList :arr="courses" :itemName="itemName" :limit="limit" @deleteItem="deleteItem" @sortItems="sortItems" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Controller from '@/components/Controller.vue';
import Modal from '@/components/UI/Modal.vue';
import ItemList from '@/components/ItemList.vue';
import { Item } from '../types/index';

export default Vue.extend({
  name: 'Courses',
  components: {
    Controller,
    Modal,
    ItemList
  },
  data () {
    return {
      title: 'Courses' as string,
      titleModal: 'Cours' as string,
      showModal: false as boolean,
      courses: [] as Item[],
      itemName: '' as string,
      limit: 5 as number
    }
  },
  methods: {
    emitModal (data: boolean) {
      this.showModal = data
    },
    createItem (data: string) {
      this.courses.push({
        name: data,
        id: Math.random(),
        isChange: false
      })
    },
    deleteItem (item: Item) {
      this.courses.splice(this.courses.indexOf(item), 1)
    },
    sortItems () {
      return this.courses.sort((a,b) => {
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
    courses: {
      deep: true,
      handler() {
         localStorage.setItem('courses', JSON.stringify(this.courses));
      }
    }
  },
  created() {
    if (localStorage.getItem('courses')) {
      this.courses = JSON.parse(localStorage.getItem('courses'));
    }
  }
})
</script>
