<template>
  <div class="home">
    <div v-for="(item, index) of items" :key="item.id">
      <HelloWorld
        :msg="item.value"
        @set-expose-function="(fn) => (componentRefs[index] = fn)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, Ref, onMounted } from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

const items = ref([
  { id: 1, value: "Welcome to Your Vue1.js + TypeScript App" },
  { id: 2, value: "Welcome to Your Vue2.js + TypeScript App" },
  { id: 3, value: "Welcome to Your Vue3.js + TypeScript App" },
]);
const componentRefs: Ref<Array<() => void>> = ref([]);

onMounted(() => {
  componentRefs.value.forEach((exposeFunction) => {
    exposeFunction();
  });
});
</script>
