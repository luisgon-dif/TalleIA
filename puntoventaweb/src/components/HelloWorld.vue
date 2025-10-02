<template>
  <section class="rounded-lg border border-dashed border-slate-300 bg-white p-6 text-center shadow-sm">
    <h2 class="text-xl font-semibold text-slate-800">{{ msg }}</h2>
    <p class="mt-3 text-sm text-slate-600">
      Esta es la base del punto de venta. A partir de aquí puedes comenzar a construir módulos,
      componentes y pantallas personalizadas para tu negocio.
    </p>
    <div class="mt-6 flex flex-wrap items-center justify-center gap-3 text-sm text-slate-500">
      <span class="rounded-full bg-slate-100 px-3 py-1">Vue 3</span>
      <span class="rounded-full bg-slate-100 px-3 py-1">TypeScript</span>
      <span class="rounded-full bg-slate-100 px-3 py-1">Tailwind CSS</span>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: {
      type: String,
      required: true
    }
  }
});
</script>
