<template>
  <div class="items_wrapper">
    <VueDraggableNext class="dragArea list-group w-full" @end="emits('changeList')" :list="data">
      <div
          v-for="(item, index) in data"
          :key="index"
          class="item"
      >
        <div class="img" :style="{'background-image': `url(${generateIMG(item.key)})`}"/>
        <div v-if="item.count" class="count" v-text="item.count"/>
      </div>
    </VueDraggableNext>

  </div>
</template>

<script setup>
import { VueDraggableNext } from 'vue-draggable-next'
const props = defineProps({
  data: { type: Array, default: [] }
});
const emits = defineEmits(['changeList'])
function generateIMG(key){
  if (!key) return ''
  switch (key){
    case 1:
      return '/images/items/green.png'
    case 2:
      return '/images/items/orange.png'
    case 3:
      return '/images/items/purple.png'
    default:
      return ''
  }
}
</script>

<style lang="scss" scoped>
.items_wrapper{
  width: 100%;
  height: 100%;
  border-radius: 12px;
  .dragArea{
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: repeat(5, 20%);
  }
  .item{
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid #4D4D4D;
    position: relative;
    cursor: pointer;
    .img{
      width: 54px;
      height: 54px;
      background-position: center;
      background-size: cover;
      background-repeat: no-repeat;
    }
    .count{
      position: absolute;
      width: 16px;
      height: 16px;
      right: -1px;
      bottom: -1px;
      border-radius: 6px 0 0 0;
      border: 1px solid #4D4D4D;
      font-size: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>
