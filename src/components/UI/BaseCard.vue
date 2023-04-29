<template>
  <div class="wrapper" :class="{active: isActivated}">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ['isActivated']
}
</script>
