<template>
  <div class="loading">
    <span class="loader"></span>
  </div>
</template>
<style scoped>
.loading {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(
    circle,
    rgba(73, 73, 73, 0.99) 30%,
    rgba(25, 25, 25, 0.99) 100%
  );
}

.loader {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 78px;
  height: 78px;
  border-radius: 50%;
  background: #fff;
  border: 8px solid #131a1d;
  overflow: hidden;
}
.loader::after {
  content: "";
  position: absolute;
  left: 0;
  top: -50%;
  width: 100%;
  height: 100%;
  background: #263238;
  z-index: 5;
  border-bottom: 8px solid #131a1d;
  box-sizing: border-box;
  animation: eyeShade 3s infinite;
}
.loader::before {
  content: "";
  position: absolute;
  left: 20px;
  bottom: 15px;
  width: 32px;
  z-index: 2;
  height: 32px;
  background: #111;
  border-radius: 50%;
  animation: eyeMove 3s infinite;
}
@keyframes eyeShade {
  0% {
    transform: translateY(0);
  }
  20% {
    transform: translateY(5px);
  }
  40%,
  50% {
    transform: translateY(-5px);
  }
  60% {
    transform: translateY(-8px);
  }
  75% {
    transform: translateY(5px);
  }
  100% {
    transform: translateY(10px);
  }
}
@keyframes eyeMove {
  0% {
    transform: translate(0, 0);
  }
  20% {
    transform: translate(0px, 5px);
  }
  40%,
  50% {
    transform: translate(0px, -5px);
  }
  60% {
    transform: translate(-10px, -5px);
  }
  75% {
    transform: translate(-20px, 5px);
  }
  100% {
    transform: translate(0, 10px);
  }
}
</style>
