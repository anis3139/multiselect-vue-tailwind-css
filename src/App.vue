<script setup lang="ts">
import Multiselect from "@/components/Multiselect.vue";
import { ref } from "vue";
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
