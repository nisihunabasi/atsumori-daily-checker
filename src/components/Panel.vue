<template>
  <div class="panel">
    <h2 class="panel-header">{{ header }}</h2>
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: {
    header: String
  },
};
</script>