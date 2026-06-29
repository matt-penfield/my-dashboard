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
  <v-app-bar flat color="white" border="b" height="72" class="px-4">
    <v-app-bar-title>
      <span class="text-h6">
        <span class="text-primary font-weight-black">FastForward</span>
        <span class="font-weight-medium">{{ title }}</span>
      </span>
    </v-app-bar-title>
    <template #append>
      <v-btn
        v-if="buttonLabel"
        color="primary"
        variant="flat"
        size="large"
        class="text-none font-weight-bold"
        @click="$emit('action')"
      >
        {{ buttonLabel }}
      </v-btn>
    </template>
  </v-app-bar>
</template>
