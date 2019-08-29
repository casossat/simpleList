<template>
  <b-container fluid id="app" >
    <img alt="Vue logo" src="./assets/logo.png">
    <hello-world-component :msg="text"/>
    <form-component @addTask="addTask"/>
    <notification-component :count="completeTask" :visibility="visibility" @setVisibility="setVisibility"/>
    <list-component :items="filterItems" @selectTask="toggleTask"/>
  </b-container>
</template>

<script lang="ts">
import Vue from "vue";
import HelloWorldComponent from "./components/HelloWorld.vue";
import FormComponent from "./components/Form.vue";
import ListComponent from "./components/List.vue";
import NotificationComponent from "./components/Notification.vue";
import { task } from "./models/task";

import PortalVue from "portal-vue";
import BootstrapVue from "bootstrap-vue";

Vue.use(BootstrapVue);
Vue.use(PortalVue);

export default Vue.extend({
  name: "app",
  components: {
    HelloWorldComponent,
    FormComponent,
    ListComponent,
    NotificationComponent
  },
  data() {
    return {
      text: "Hello World!",
      items: [
        { id: 0, text: "Task_0", complete: true },
        { id: 1, text: "Task_1", complete: false },
        { id: 2, text: "Task_2", complete: true },
        { id: 3, text: "Task_3", complete: true },
        { id: 4, text: "Task_4", complete: false }
      ] as task[],
      visibility: "all"
    };
  },
  computed: {
    orderList(): task[] {
      return this.items.slice(0).reverse();
    },
    completeTask(): Number {
      return this.items.filter(x => x.complete).length;
    },
    filterItems(): task[] {
      return this.orderList.filter((item: task) => {
        if (this.visibility == "all") return item;
        if (this.visibility == "active") return !item.complete;
        return item.complete;
      });
    }
  },
  methods: {
    addTask(newTask: string): void {
      if (newTask.length)
        this.items.push({
          id: this.items.length + 1,
          text: newTask,
          complete: false
        });
    },
    toggleTask(item: task): void {
      item.complete = !item.complete;
    },
    setVisibility(status: String): void {
      this.visibility = status;
    }
  }
});
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
