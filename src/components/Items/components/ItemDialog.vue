<template>
    <div v-if="modelValue" class="item_dialog_wrapper">
      <div class="content">
        <div @click="emits('update:modelValue', false)" class="close">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M18 7.05L16.95 6L12 10.95L7.05 6L6 7.05L10.95 12L6 16.95L7.05 18L12 13.05L16.95 18L18 16.95L13.05 12L18 7.05Z" fill="white"/>
          </svg>
        </div>
        <div class="up">
          <div class="img" :style="{'background-image': `url(${generateIMG(data.key)})`}" />
          <div class="text">asd</div>
        </div>
        <div v-if="data.count" class="actions">
          <button
              v-if="!deleteActions"
              class="delete_btn"
              @click="deleteActions = true"
          >
            Удалить предмет
          </button>
          <div v-else class="approve">
            <input v-model="deleteActionsCount" placeholder="Введите количество"/>
            <div class="btns">
              <button class="cancel" @click="reset">Отмена</button>
              <button class="check" @click="approve">Подтвердить</button>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script setup>

import {ref} from "vue";

const props = defineProps({
  modelValue: { type: Boolean, default: false },
  data:       { type: Object, default: {} }
})
const emits = defineEmits(['update:modelValue', 'deleteCount']);

const deleteActions = ref(false);
const deleteActionsCount = ref(null)

function generateIMG(key) {
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
function approve() {
  if (!deleteActionsCount.value || +deleteActionsCount.value > props.data.count || !isNAN(+deleteActionsCount.value)) return ''
  emits('deleteCount', { ...props.data, count: props.data.count - +deleteActionsCount.value });
  deleteActions.value = false;
  deleteActionsCount.value = null;
}

function reset() {
  deleteActions.value = false;
  deleteActionsCount.value = null;
}

function isNAN(value) {
  if(value instanceof Number)
    value = value.valueOf();

  return  isFinite(value) && value === parseInt(value, 10);
}
</script>

<style lang="scss">
.item_dialog_wrapper{
  position: absolute;
  max-width: 250px;
  width: 100%;
  height: 100%;
  border: 1px solid #4D4D4D;
  right: 0;
  top: 0;

  .content{
    position: relative;
    width: 100%;
    height: 100%;
    padding: 10px;
    backdrop-filter: blur(10px);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;

    .img{
      width: 130px;
      height: 130px;
      background-size: cover;
      background-repeat: no-repeat;
      background-position: center;
      margin: 50px auto 20px;
    }


    .text{
      padding: 5px 0;
      margin: 5px 0;
      border-top: 1px solid #4D4D4D;
      border-bottom: 1px solid #4D4D4D;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .up{
      width: 100%;
    }
    .actions{
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
    }

    .close{
      position: absolute;
      top: 5px;
      right: 5px;
      cursor: pointer;
    }
    .delete_btn{
      margin-top: 5px;
      max-width: 220px;
      width: 100%;
      height: 39px;
      border-radius: 8px;
      background: #FA7272;
      border: none;
      color: white;
      cursor: pointer;
    }

    .approve{
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;

      input {
        width: 100%;
        background-color: transparent;
        border: 1px solid #4D4D4D;
        color: white;
        outline: none;
        padding: 10px;
        border-radius: 8px;
      }

      .btns {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        margin-top: 15px;

        .cancel,
        .check{
          border: none;
          cursor: pointer;
          border-radius: 8px;
          width: 45%;
          padding: 10px;
        }

        .cancel {
          background: #FFFFFF;
          color: #1c1c1c;

        }

        .check {
          background: #FA7272;
          color: white;
        }
      }
    }
  }
}

</style>
