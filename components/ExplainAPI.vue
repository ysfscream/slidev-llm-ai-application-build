<script setup lang="ts">
import { ref, computed, watch, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const click = ref<number | null>(null)

defineProps({
  content: {
    required: true,
    type: Array,
    default: () => ([])
  },
})

const route = useRoute()

const clicks = computed(() => route.query.clicks)

watch(clicks, (newVal) => {
  if (newVal && typeof newVal === 'string') {
    click.value = parseInt(newVal, 10)
  } else {
    click.value = null
  }
})

onMounted(() => {
  if (clicks.value && typeof clicks.value === 'string') {
    click.value = parseInt(clicks.value, 10)
  }
})
</script>

<template>
  <p v-if="click !== null">{{ content[click - 1] }}</p>
</template>