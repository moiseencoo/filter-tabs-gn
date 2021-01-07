<template>
  <div class="button-preloader"><div></div><div></div><div></div><div></div></div>
</template>

<script>
export default {

}
</script>

<style scoped>
.button-preloader {
  display: inline-block;
  position: relative;
  width: 100%;
  height: 10px;
}
.button-preloader div {
  position: absolute;
  top: 6px;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #fff;
  animation-timing-function: cubic-bezier(0, 1, 1, 0);
}
.button-preloader div:nth-child(1) {
  left: 14px;
  animation: button-preloader1 0.6s infinite;
}
.button-preloader div:nth-child(2) {
  left: 14px;
  animation: button-preloader2 0.6s infinite;
}
.button-preloader div:nth-child(3) {
  left: 38px;
  animation: button-preloader2 0.6s infinite;
}
.button-preloader div:nth-child(4) {
  left: 62px;
  animation: button-preloader3 0.6s infinite;
}
@keyframes button-preloader1 {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes button-preloader3 {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
@keyframes button-preloader2 {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(24px, 0);
  }
}
</style>