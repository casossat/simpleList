<template>
  <div>
    <b-input-group size="lg">
      <b-form-input type="text" v-model="newTask" placeholder="Add new task..."></b-form-input>
      <b-input-group-append>
        <b-button variant="info" @click="addTask" :disabled="!newTask.length">Add</b-button>
      </b-input-group-append>
    </b-input-group>
    <!--<input type="text" v-model="newTask" placeholder="Add new task...">
    <button class="btn btn-primary" @click="$emit('addTask', newTask)">Add</button>-->

    <!--<input type="text" v-model="newTask" placeholder="Add new task..." @keyup.enter="$emit('addTask', newTask)">-->

    <!--<input type="text" v-model="newTask" placeholder="Add new task..." @keyup.enter="addTask">

    <input type="text" v-model="newTask" placeholder="Add new task...">
    <button class="btn btn-primary" @click="addTask" :disabled="!newTask.length">Add</button>-->
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "FormTask",
  data() {
    return {
      newTask: ""
    };
  },
  methods: {
    addTask(): void {
      this.$emit("addTask", this.newTask);
      this.newTask = "";
    }
  }
});
</script>

<style>
.input-test input {
  height: 34px;
  width: 75%;
  outline: none;
  padding: 2px 5px;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
}
.input-test button {
  height: 42px;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
}
</style>
