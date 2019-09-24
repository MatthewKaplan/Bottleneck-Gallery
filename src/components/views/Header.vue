<template>
  <header class="header">
    <h1 @click="$emit('return-btn')">Bottleneck Gallery</h1>
    <img @click="$emit('return-btn')" class="logo" src="../../assets/BNG-logo.png" />
  </header>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style scoped>
.header {
  display: flex;
  background: #fff;
  color: #fff;
  text-align: center;
  padding: 10px;
  border-bottom: 1px solid #333;
  justify-content: space-between;
}

.header h1 {
  color: #000;
  font-size: 45px;
  align-self: flex-end;
  cursor: pointer;
}

.logo {
  height: 75px;
  width: 10%;
  cursor: pointer;
}

@media screen and (max-width: 500px) {
  .header h1 {
    font-size: 28px;
  }

  .logo {
    height: 65px;
    width: 16%;
  }
}
</style>


