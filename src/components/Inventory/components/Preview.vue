<template>
  <div class="preview_wrapper">
    <template v-if="loading">
      <Skeleton class="q-mx-auto q-mb-md" width="208px" height="240px"/>
      <Skeleton class="q-mx-auto q-mb-md" width="190px" height="26px" />
      <Skeleton class="q-mx-auto q-mb-md" width="208px" height="10px"/>
      <Skeleton class="q-mx-auto q-mb-md" width="208px" height="10px"/>
      <Skeleton class="q-mx-auto q-mb-md" width="208px" height="10px"/>
    </template>
    <template v-else>
      <div class="img" :style="{'background-image': `url(${props.imageURL})`}"/>
      <div class="content">
        <p class="title" v-text="props.title"/>
        <p class="description" v-text="props.description"/>
      </div>
    </template>
  </div>
</template>

<script setup>
import Skeleton from "@/components/Skeleton";

const props = defineProps({
  imageURL:    { type: String, default: '' },
  title:       { type: String, default: '' },
  description: { type: String, default: '' },
  loading:     { type: Boolean, default: false },
})
</script>

<style lang="scss" scoped>
.preview_wrapper{
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-direction: column;
  .img{
    max-width: 208px;
    width: 100%;
    height: 240px;
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    border-radius: 8px;
  }
  .title{
    font-weight: bold;
  }
  .title,
  .description{
    text-align: center;
  }
}
</style>
