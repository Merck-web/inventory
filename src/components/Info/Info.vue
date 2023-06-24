<template>
  <div class="info_wrapper">
    <div @click="emits('close')" class="close">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M18 7.05L16.95 6L12 10.95L7.05 6L6 7.05L10.95 12L6 16.95L7.05 18L12 13.05L16.95 18L18 16.95L13.05 12L18 7.05Z" fill="white"/>
      </svg>
    </div>
    <template v-if="loading">
      <Skeleton width="95%" height="36px" no-center/>
    </template>
    <template v-else>
      <p class="description" v-text="description"/>
    </template>
  </div>
</template>

<script setup>
import Skeleton from "@/components/Skeleton";

const props = defineProps({
  loading:     { type: Boolean, default: false },
  description: { type: String, default: '' }
});
const emits = defineEmits(['close']);
</script>

<style lang="scss" scoped>
.info_wrapper{
  position: relative;

  .close{
    position: absolute;
    content: '';
    right: -5px;
    top: -10px;
    width: 24px;
    height: 24px;
    cursor: pointer;
  }

  .description{

  }
}
</style>
