<template>
  <b-container>
    <b-list-group>
      <b-list-group-item v-for="(item, idx) in items" :key="idx" 
      @click="$emit('selectTask', item)" :class="{ active: item.complete }"> 
        {{ item.text }} 
      </b-list-group-item>
    </b-list-group>
  </b-container>
</template>

<script lang="ts">
import Vue from "vue";
import { task } from "../models/task";

export default Vue.extend({
  name: "List",
  props: {
    items: {
      type: Array as () => task[],
      required: true
    }
  }
});
</script>

