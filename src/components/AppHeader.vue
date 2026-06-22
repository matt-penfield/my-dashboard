<script setup lang="ts">
defineProps<{
  title: string
  buttonLabel?: string
}>()

defineEmits<{
  action: []
}>()
</script>

<template>
  <header class="app-header">
    <h1><span>FastForward</span> {{ title }}</h1>
    <button v-if="buttonLabel" class="btn-primary" @click="$emit('action')">
      {{ buttonLabel }}
    </button>
  </header>
</template>

<style scoped>
.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 28px;
  flex-wrap: wrap;
  gap: 12px;
}

.app-header h1 {
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: -0.02em;
}

.app-header h1 span {
  color: var(--primary);
}

.btn-primary {
  background: var(--primary);
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 8px;
  font-size: 0.875rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}

.btn-primary:hover {
  background: #1d4ed8;
}

@media (max-width: 480px) {
  .app-header h1 {
    font-size: 1.25rem;
  }
}
</style>
