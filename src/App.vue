<template>
  <header>
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/game">Play Game</router-link>
    </nav>
  </header>
  <router-view></router-view>
</template>

<style>
header { background: #333; padding: 1rem; }
nav { display: flex; gap: 20px; justify-content: center; }
nav a { color: white; text-decoration: none; font-weight: bold; }
nav a.router-link-active { color: #42b983; }
body { margin: 0; font-family: sans-serif; background: #f4f4f4; }
</style>