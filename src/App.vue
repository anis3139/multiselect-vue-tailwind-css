<template>
  <div class="text-light">
    {{options}}
    <Multiselect
      v-model="value"
      mode="tags"
      placeholder="Select your characters"
      :options="options"
      :searchable="true"
      :createTag="true"
      style="min-width: 300px"
    />
  </div>
</template>

<script>
import Multiselect from "@vueform/multiselect";

export default {
  components: { Multiselect },
  data() {
    return {
      value: ["Batman"],
      options: ["Batman", "Robin", "Joker"],
    };
  },
};
</script>

<style src="@vueform/multiselect/themes/default.css"></style>
