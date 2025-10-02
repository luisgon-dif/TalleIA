<template>
  <div class="min-h-screen bg-slate-50 text-slate-900">
    <header class="bg-white shadow">
      <div class="mx-auto max-w-6xl px-4 py-6">
        <h1 class="text-2xl font-bold">Punto de Venta</h1>
        <p class="text-sm text-slate-500">Proyecto inicial en Vue 3 + TypeScript + Tailwind CSS</p>
      </div>
    </header>
    <main class="mx-auto max-w-6xl px-4 py-10">
      <HelloWorld msg="Bienvenido al punto de venta" />
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld
  }
});
</script>
