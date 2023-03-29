<template>
  <div
    class="home"
    v-for="item of items"
    :key="item.id"
    :ref="setComponentRefs"
  >
    <HelloWorld :msg="msg" ref="componentRef" />
  </div>
  <button @click="onFire">Fire</button>
</template>

<script setup lang="ts">
import { ref } from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

const msg = ref("hello world");
const componentRefs = ref<Array<InstanceType<typeof HelloWorld>>>([]);

const items = ref([
  { id: "001", value: "vue1" },
  { id: "002", value: "vue2" },
  { id: "003", value: "vue3" },
]);
// eslint-disable-next-line @typescript-eslint/no-explicit-any
function setComponentRefs(el: any) {
  if (el) {
    componentRefs.value.push(el as InstanceType<typeof HelloWorld>);
  }
}
function onFire() {
  componentRefs.value.forEach((componentRef) => {
    componentRef.exposeFunction();
  });
}
</script>
