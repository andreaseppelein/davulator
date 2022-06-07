<template>
  <div class="flex-1 px-2 py-2 justify-center flex items-center text-white text-2xl font-semibold">
    <div
      class="rounded-full h-20 w-20 flex items-center bg-purple-800 justify-center shadow-lg border-2 border-purple-700 hover:border-2 hover:border-gray-500 focus:outline-none"
      @click="emitIfPossible"
    >{{ buttonLabel }}</div>
  </div>
</template>

<script setup lang="ts">

import { computed } from 'vue';

interface Props {
  type: string
  value: string
}

interface ValueMapping {
  key: string
  label?: string
  value?: string
}

const valueMappings: ValueMapping[] = [
  { key: 'division', label: '÷', value: '/' },
  { key: 'multiplication', label: '×', value: '*' },
  { key: 'addition', label: '+', value: '+' },
  { key: 'subtraction', label: '-', value: '-' },
  { key: 'calculate', label: '=', value: '=' },
  { key: 'reset', label: 'C', value: 'C' }
]

const props = defineProps<Props>()

const buttonLabel = computed(() => {
  switch(props.type) {
    case 'operator': return valueMappings.find((item) => item.key === props.value)?.label
    case 'action': return valueMappings.find((item) => item.key === props.value)?.label
    case 'placeholder': return ''
    default: return props.value
  }
})

const emit = defineEmits<{
  (e: 'addToExpression', char: string | undefined): void
}>()

function emitIfPossible() {
  if (props.type === 'number' || props.type === 'decimal') {
    emit('addToExpression', props.value)
  }

  if (props.type === 'operator') {
    emit('addToExpression', ` ${valueMappings.find((item) => item.key === props.value)?.value} `)
  }
}
</script>
