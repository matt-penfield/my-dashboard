<script setup lang="ts">
const open = defineModel<boolean>({ required: true })
</script>

<template>
  <v-dialog v-model="open" max-width="600">
    <v-card>
      <v-card-text>
        <slot />
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn variant="text" @click="open = false">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
