<script setup lang="ts">
import type { FieldProps } from './interface'
import { FormControl } from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import { Textarea } from '@/components/ui/textarea'
import { computed } from 'vue'

const props = defineProps<FieldProps & {
  componentField: any
}>()
const inputComponent = computed(() => props.config?.component === 'textarea' ? Textarea : Input)
</script>

<template>
  <component
    :is="inputComponent"
    type="text"
    v-bind="{ ...componentField, ...config?.inputProps }"
    :disabled="disabled"
  />
</template>
