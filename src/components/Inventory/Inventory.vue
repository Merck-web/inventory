<template>
  <div class="invent_wrapper">
    <div class="preview">
      <Preview
          :imageURL="targetItem.imageURL"
          :title="targetItem.title"
          :description="targetItem.description"
          :loading="loading"
      />
    </div>
    <div class="items">
      <Items
          :data="itemsInvent"
          :loading="loading"
          @changeList="updateChangeList"
          @deleteCount="deleteCount"
      />
    </div>
    <div
        v-if="infoVisible"
        class="info"
    >
      <Info
          :loading="loading"
          :description="'hasdjhbasd asdjhasgdijb sadkjhasid askdhujaskd'"
          @close="infoVisible = false"
      />
    </div>
  </div>
</template>

<script setup>
import {onMounted, ref} from 'vue';
import Preview from "@/components/Inventory/components/Preview";
import Info from "@/components/Info/Info";
import Items from "@/components/Items/Items";

const targetItem = ref({
  imageURL: '/images/preview/preview.png',
  title: 'Крутая шмотка',
  description: 'Нереально крутая шмотка',
})
const itemsInvent = ref([
  { key: 1, count: 4 },
  { key: 2, count: 4 },
  { key: 3, count: 4 },
  { key: 2, count: 4 },
  { key: 1, count: 4 },
])
const different = 25 - itemsInvent.value.length;
for (let i = 0; i < different; i++){
  itemsInvent.value.push({ key: 0, count: 0 })
}
const loading = ref(true);
const infoVisible = ref(true);

onMounted(async _=>{
  await new Promise(v => setTimeout(v, 1000));
  const inventory = JSON.parse(localStorage.getItem('inventory')) || [];
  if (!inventory.length) localStorage.setItem('inventory', JSON.stringify(itemsInvent.value));
  else itemsInvent.value = inventory;
  loading.value = false;
})
function updateChangeList(){
  localStorage.setItem('inventory', JSON.stringify(itemsInvent.value))
}
function deleteCount(newData){
  itemsInvent.value[newData.index] = newData.newObj;
  if (itemsInvent.value[newData.index].count <= 0){
    itemsInvent.value[newData.index] = { key: 0, count: 0 }
  }
  updateChangeList()
}
</script>

<style lang="scss" scoped>
.invent_wrapper {
  display: grid;
  grid-template-areas:
        "preview items"
        "info info";
  gap: 15px;
  grid-template-columns: 236px auto;
  grid-template-rows: 500px 72px;

  .preview {
    grid-area: preview;
    max-width: 236px;
    width: 100%;
  }

  .items {
    grid-area: items;
  }

  .info {
    grid-area: info;
  }

  .preview,
  .items,
  .info {
    border-radius: 12px;
    padding: 15px;
    border: 1px solid #4D4D4D;
    background:  linear-gradient(0deg, #262626, #262626);
  }
}
</style>
