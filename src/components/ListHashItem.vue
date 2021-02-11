<template>
    <li class="list-group-item animate-li li-item" @click="$emit('removeItem', item)" title="Click to remove">{{ item }}</li>
</template>

<script>

    export default {
        name: "ListHashItem",

      props:{
            item:{
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>
.li-item:hover{
  background-color: #6c757d;
  cursor: pointer;
  color: #eff2f1;
}
.animate-li {

  animation: trAnimate 1s linear;
}
@keyframes trAnimate {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}
</style>