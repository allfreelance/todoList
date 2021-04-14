<template>
  <nav class="bg-green-500 text-white">
    <div class="container mx-auto">
      <div class="flex items-center">
        <router-link to="/" class="inline-block px-16 py-4 transition-colors hover:bg-green-700 duration-300">Home</router-link>
        <router-link to="todos" class="inline-block px-16 py-4 transition-colors hover:bg-green-700 duration-300">Todos</router-link>
      </div>
    </div>
  </nav>
  
  <router-view/>
</template>

<style>
body {
  background-color: rgb(214, 214, 214);
}
.router-link-active {
  @apply bg-green-700
}
</style>
