<template>
  <b-container fluid class="notification-test">
    <b-row>
      <b-col>
        <span v-if="!count">Great! You don't have any task</span>
        <span v-else>{{ count }} {{ count | pluralize }} to do....</span>
      </b-col>
    </b-row>

    <b-row>
      <b-col>
        <b-button-group size="sm">
          <b-button variant="success" @click="setVisibility('all')">All</b-button>
          <b-button variant="info" @click="setVisibility('active')">Active</b-button>
          <b-button variant="warning" @click="setVisibility('complete')">Complete</b-button>
        </b-button-group>
      </b-col>
    </b-row>
  </b-container>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "HelloWorld",
  data() {
    return {
      newTask: ""
    };
  },
  filters: {
    pluralize(count: Number): String {
      return count == 1 ? 'task' : 'tasks'
    }
  },
  props: {
    count: {
      type: Number,
      required: true
    },
    visibility: {
      type: String,
      required: true
    }
  },
  methods: {
    setVisibility(status: String): void {
      this.$emit("setVisibility", status);
    }
  }
});
</script>

<style>
.notification-test {
  font-weight: 600;
  margin: 16px 0;
}
</style>
