<script setup lang="ts">
import { ref } from "vue";
import Multiselect from "./components/Multiselect.vue";
const options = ref(["admin", "editor", "author", "user"]);
const selected = ref(["admin", "editor"]);
</script>

<template>
  <Multiselect
    :options="options"
    v-model="selected"
    placeholder="Pick some..."
    class="block w-full"
  ></Multiselect>
</template>
