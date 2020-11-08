<template>
  <h1>{{ count }}</h1>
  <h1>{{ name }}</h1>
  <p>{{ id }}</p>
  <button @click="add">add</button>
  <button @click="reduce">reduce</button>
</template>

<script lang="ts">
import { reactive, toRefs, computed, watch } from "vue";
import { useRoute } from "vue-router";

export default {
  name: "Page",
  setup() {
    const state = reactive({
      count: 0,
      name: "jack",
    });

    const route = useRoute();

    let id = computed(() => {
      return route.query.id;
    });

    watch(
      [() => state.count, () => state.name],
      ([newCount, oldCount], [newName, oldName]) => {
        console.log(newCount, "=====", oldCount);
        console.log(newName, "=====", oldName);
      },
      { immediate: true }
    );

    setInterval(() => {
      state.count++;
      state.name = "yony";
    }, 1000);
    // watch(
    //   () => state.count,
    //   (newVal, old) => {
    //     console.log(newVal, old);
    //   },
    //   { immediate: true }
    // );

    const add = () => {
      state.count++;
    };

    const reduce = () => {
      state.count--;
    };

    return {
      ...toRefs(state),
      id,
      add,
      reduce,
    };
  },
};
</script>

<style></style>
