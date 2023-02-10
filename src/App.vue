<script setup>

</script>

<template>
  <header>
    <div>
        <img src="./assets/poke-logo.png" alt="Logo" class="d-inline-block align-text-top">
    </div>
    </header>

  <div class="main">
    <router-view></router-view>
  </div>

  <footer>
    <img src="./assets/poke-favicon.png" alt=""><img src="./assets/poke-logo.png" alt=""> <img src="./assets/poke-favicon.png" alt="" />
  </footer>
</template>

<style>
body{
  overflow: hidden;
  min-height: 100vh;
  background: #FB1B1B;
}


header {
  display: flex;
  justify-content: center;
}

header div img {
  width: 200px;
}



footer{
  background-color: #FB1B1B;
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 40px;
  display: flex;
  align-items:center;
  justify-content: center;
}

footer img {
  width: 60px;
  margin-bottom: 20px;
  padding: 10px;
}

footer img:nth-child(2) {
  width: 150px;
}
@media (max-width: 600px) {
  body{
    overflow: auto;
  }
}
</style>