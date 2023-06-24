<template>
  <div class="items_wrapper">
    <template v-if="loading">
      <Skeleton width="100%" height="100%"/>
    </template>
    <template v-else>
      <VueDraggableNext class="dragArea list-group w-full" @end="emits('changeList')" :list="data">
        <div
            v-for="(item, index) in data"
            :key="index"
            class="item"
            @click="openInfoDialog(item, index)"
        >
          <div class="img" :style="{'background-image': `url(${generateIMG(item.key)})`}"/>
          <div v-if="item.count" class="count" v-text="item.count"/>
        </div>
      </VueDraggableNext>
    </template>


    <ItemDialog
        :model-value="itemsInfoDialog"
        :data="infoDataItems"
        @update:model-value="newValue => itemsInfoDialog = newValue"
        @deleteCount="deleteCount"
    />
  </div>
</template>

<script setup>
import { VueDraggableNext } from 'vue-draggable-next'
import ItemDialog from "@/components/Items/components/ItemDialog";
import {ref} from "vue";
import Skeleton from "@/components/Skeleton";

const props = defineProps({
  data:    { type: Array, default: [] },
  loading: { type: Boolean, default: false }
});
const emits = defineEmits(['changeList', 'deleteCount']);

const itemsInfoDialog = ref(false);
const infoDataItems   = ref({});
const changeItemIndex = ref(null);

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
function openInfoDialog(item, index) {
  if (!item.count || !item.key) return
  infoDataItems.value   = item;
  changeItemIndex.value = index;
  itemsInfoDialog.value = true;
}
function deleteCount(newObj) {
  emits('deleteCount', {index: changeItemIndex.value, newObj: newObj});
  itemsInfoDialog.value = false;
  infoDataItems.value   = {};
  changeItemIndex.value = null;
}
</script>

<style lang="scss" scoped>
.items_wrapper{
  width: 100%;
  height: 100%;
  border-radius: 12px;
  position: relative;
  overflow: hidden;
  padding: 5px;
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
