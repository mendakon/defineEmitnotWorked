<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, onMounted } from "vue";

interface Props {
  msg: string;
}
const props = defineProps<Props>();

interface Emits {
  (e: "setExposeFunction", fn: () => void): void;
}
const emit = defineEmits<Emits>();

const exposeFunction = () => {
  console.log(props.msg);
};
onMounted(() => {
  emit("setExposeFunction", exposeFunction);
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
