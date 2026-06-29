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
  <v-app-bar flat color="white" border="b">
    <v-app-bar-title>
      <span class="text-primary font-weight-bold">FastForward</span>
      {{ title }}
    </v-app-bar-title>
    <template #append>
      <v-btn
        v-if="buttonLabel"
        color="primary"
        variant="flat"
        @click="$emit('action')"
      >
        {{ buttonLabel }}
      </v-btn>
    </template>
  </v-app-bar>
</template>
