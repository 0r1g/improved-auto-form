<script setup lang="ts">
import type { FieldProps } from './interface'
import { FormControl } from '@/components/ui/form'
import { Input } from '@/components/ui/input'

defineOptions({
  inheritAttrs: false,
})

defineProps<FieldProps & {
  componentField: any
}>()
</script>

<template>
  <Input type="number" v-bind="{ ...componentField, ...config?.inputProps }" :disabled="disabled" />
</template>
