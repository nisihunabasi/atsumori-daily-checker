<template>
  <label>
    <input type="checkbox" />
    <span v-if="!slim">&nbsp;</span>{{ refLabel }}
  </label>
</template>

<script>
import {ref} from "vue"
export default {
  props: {
    slim: {
      type: Boolean,
      default: false
    },
    label: {
      type: String
    }
  },
  setup(props) {
    const refLabel = ref(props.label);
    return {
      refLabel,
    }
  },
};
</script>
