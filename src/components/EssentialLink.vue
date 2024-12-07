<template>
  <q-item clickable :tag="isExternalLink ? 'a' : 'router-link'" :href="isExternalLink ? link : undefined"
    :to="!isExternalLink ? link : undefined" :target="isExternalLink ? '_blank' : undefined">
    <q-item-section v-if="props.icon" avatar>
      <q-icon :name="props.icon" />
    </q-item-section>

    <q-item-section>
      <q-item-label>{{ props.title }}</q-item-label>
      <q-item-label caption>{{ props.caption }}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  title: {
    type: String,
    required: true
  },

  caption: {
    type: String,
    default: ''
  },

  link: {
    type: String,
    default: '#'
  },

  icon: {
    type: String,
    default: ''
  }
})

const isExternalLink = computed(() => {
  // If the link contains "http" or starts with "//", treat it as external
  return props.link.startsWith('http') || props.link.startsWith('//')
})
</script>
