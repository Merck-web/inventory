<template>
  <div class="skeleton_wrapper">
    <div
        class="load"
        :style="{
            maxWidth:        props.width,
            height:          props.height,
            borderRadius:    props.br,
            margin:          props.noCenter ? '0px' : '0 auto'
        }"
    />
  </div>
</template>

<script setup>
const props = defineProps({
  width:       { type: String, default: '1920px' },
  height:      { type: String, default: '' },
  br:          { type: String, default: '8px' },
  noCenter:    { type: Boolean, default: false },
})
</script>

<style lang="scss" scoped>
.skeleton_wrapper{
  width: 100%;
  height: 100%;

  .load {
    position: relative;
    background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
    width: 100%;
    margin: 0 auto;
    overflow: hidden;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.11);
    &::after {
      display: block;
      content: '';
      position: absolute;
      width: 100%;
      height: 100%;
      transform: translateX(-100%);
      background: linear-gradient(
              90deg,
              transparent,
              rgba(#fff, 0.35),
              transparent
      );
      animation: loading 1.5s infinite;
    }
    @keyframes loading {
      100% {
        transform: translateX(100%);
      }
    }
  }
}
</style>
