<!--
  IconBadge — fondo con forma, tinteado con la paleta, que envuelve un glifo de icono.
  Fuente única del estilo de los badges del deck. Generado por /slides illustrate.

  El glifo va como slot con clase estática de UnoCSS (i-ph:...), para que la
  extracción estática de UnoCSS lo detecte. NO construir la clase en runtime.

  Uso:
    <IconBadge shape="squircle" size="md"><div class="i-ph:scissors" /></IconBadge>
-->
<script setup>
defineProps({
  shape: { type: String, default: 'circle' }, // circle | squircle
  size:  { type: String, default: 'md' },     // sm | md | lg
})
</script>

<template>
  <div class="icon-badge" :class="[`shape-${shape}`, `size-${size}`]">
    <slot />
  </div>
</template>

<style scoped>
.icon-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex: none;
  background: color-mix(in srgb, var(--c-accent) 12%, transparent);
  color: var(--c-accent);
}
.icon-badge :deep(> *) {
  width: 58%;
  height: 58%;
}
.shape-circle   { border-radius: 9999px; }
.shape-squircle { border-radius: 28%; }
.size-sm { width: 2.25rem; height: 2.25rem; }
.size-md { width: 3.25rem; height: 3.25rem; }
.size-lg { width: 4.75rem; height: 4.75rem; }
</style>
