<template>
  <h3>{{ count }}</h3>
</template>

<script lang="ts">
import { ref, watch } from "vue";
export default {
  name: "About",
  setup() {
    let count = ref(0);

    watch(count, (newVal, oldVal) => {
      console.log("new", newVal, "old", oldVal);
    });

    setInterval(() => {
      count.value++;
    }, 1000);
    return {
      count,
    };
  },
};
</script>

<style></style>
