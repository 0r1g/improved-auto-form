<script setup lang="ts">
import type { FieldProps } from './ui/improved-auto-form/interface'

defineProps<FieldProps & {
    options?: string[]
    componentField: any
}>()
</script>

<template>
    <div>
        <label>{{ config?.label }}</label>
        <input v-bind="{ ...componentField }" :disabled="disabled" />
    </div>
</template>
