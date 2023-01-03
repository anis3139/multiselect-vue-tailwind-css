<script setup lang="ts">
import { computed, ref, watch } from "vue";
const emit = defineEmits(["update:input"]);
const props = defineProps({
  options: {
    type: Array,
    default: [],
    require: false,
  },
  modelValue: {
    type: Array,
    default: [],
    require: false,
  },

  placeholder: {
    type: String,
    default: "Select one",
    require: false,
  },
});

watch(props.modelValue, async (newVal, oldVal) => {
  emit("update:input", newVal);
});

const optionObj = computed(() => {
  let result = props.options.map((option) => {
    let checked = props.modelValue.includes(option);
    return { value: option, checked: checked };
  });

  return result;
});
const toggle = ref(false);

const toggler = () => {
  toggle.value = !toggle.value;
};

const removeHandaler = (item: string) => {
  props.modelValue.splice(props.modelValue.indexOf(item), 1);
};

const itemHandeler = (option: { value: string; checked: boolean }) => {
  var index = props.modelValue.indexOf(option.value);

  if (index === -1) {
    props.modelValue.push(option.value);
  } else {
    props.modelValue.splice(index, 1);
  }
};
</script>

<template>
  <div>
    <div
      aria-level="parent"
      class="relative"
      @blur="toggle = false"
      tabindex="-1"
    >
      <div
        aria-level="input_box"
        class="p-1 form-controll outline outline-gray-200 dark:outline-gray-600"
        @click="toggler"
      >
        <div v-if="modelValue.length > 0">
          <div
            v-for="sd in modelValue"
            :key="sd"
            class="inline-flex flex-wrap items-center"
          >
            <div
              class="max-w-fit mr-2 py-0.5 px-2 min-w-7 h-7 inline-flex items-center rounded-lg bg-gray-700 text-white hover:bg-gray-800 my-0.5"
            >
              <span class="mr-2 text-md">{{ sd }}</span>
              <span
                class="text-sm mt-0.5 inline-block cursor-pointer hover:font-bold text-red-800 hover:text-red-700 hover:scale-105"
                @click.prevent.stop="removeHandaler(sd)"
                >&#x2717;</span
              >
            </div>
          </div>
        </div>
        <div v-else class="text-gray-700 shadow-sm h-7">
          {{ placeholder }}
        </div>
      </div>
      <transition
        enter-active-class="transition ease-out duration-200"
        enter-from-class="transform opacity-0 scale-95"
        enter-to-class="transform opacity-100 scale-100"
        leave-active-class="transition ease-in duration-75"
        leave-from-class="transform opacity-100 scale-100"
        leave-to-class="transform opacity-0 scale-95"
      >
        <div
          aria-level="output_box"
          class="w-full h-32 overflow-scroll bg-gray-200 dark:bg-gray-300 p-2 absolute z-50 mt-2 rounded-sm shadow-lg"
          v-show="toggle"
        >
          <div
            v-for="option in optionObj"
            :key="option"
            @click="itemHandeler(option)"
          >
            <div
              class="w-full min-h-8 mt-2 flex gap-2 items-center p-2 rounded-md ring-1 ring-black ring-opacity-5 text-black bg-gray-400 hover:bg-gray-300 dark:bg-gray-900 dark:hover:bg-gray-800 dark:text-white cursor-pointer"
            >
              <div class="grid place-item-center">
                <span
                  class="checked grid place-content-center text-sm"
                  v-if="option.checked"
                  >&#x2713;</span
                >
                <span v-else class="unChecked"></span>
              </div>
              <div class="break-all">
                {{ option.value }}
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>
