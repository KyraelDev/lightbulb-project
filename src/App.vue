<template>
  <header>
    <div>
      <nav class="h-[40px] flex justify-start items-center p-4 mx-6 bg-black text-white relative z-40 testo-omori-game2">
        <RouterLink class="m-4 testo-omori-game2" to="/">Home</RouterLink>
        <RouterLink class="m-4 testo-omori-game2" to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
  <footer class="absolute bottom-0 left-0 w-full overflow-hidden">
  <div class="testo-omori-game2">
    <div class="h-[40px] flex justify-start items-center px-4 mx-6 bg-black text-white relative z-40 text-[20px]">
      Copyright KyraDev 2024 ~ Marcello A. Licciardello
    </div>
  </div>
</footer>

</template>

<script>
import { RouterLink, RouterView } from 'vue-router'

export default {
}
</script>

<style>
.testo-omori-game2 {
  font-family: 'OmoriGame2', sans-serif;
  font-size: xx-large;
}

.custom-cursor {
  cursor: url('../assets/imgs/cursorebase.png'), auto;
}
</style>
