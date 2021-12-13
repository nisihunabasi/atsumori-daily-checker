<template>
  <label>
    <input type="checkbox" v-model="isChecked"/>
    <span v-if="!slim">&nbsp;</span>{{ refLabel }}
  </label>
</template>

<script>
import { ref, computed } from "vue"

export default {
  props: {
    slim: {
      type: Boolean,
      default: false
    },
    label: {
      type: String
    },
    modelValue: {
      type: Array
    }
  },
  emits: ["update:modelValue"],
  setup(props, {emit}) {
    const refLabel = ref(props.label);
    const isChecked = computed({
      get: () => (props.modelValue.indexOf(props.label) !== -1),
      set: val => {
        let checkedTasks = props.modelValue.slice(0);
        if (val) {
          if (checkedTasks.indexOf(props.label) == -1) {
            checkedTasks.push(props.label);
            emit("update:modelValue", checkedTasks);
          }
        } else {
          let idx = checkedTasks.indexOf(props.label);
          if (idx !== -1) {
            checkedTasks.splice(idx, 1);
            emit("update:modelValue", checkedTasks);
          }
        }
      }
    })
    return {
      isChecked,
      refLabel,
    }
  },
};
</script>
