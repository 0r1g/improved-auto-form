<script setup lang="ts">
import type { FieldProps } from './interface'
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select'
import { beautifyObjectName } from './utils'

defineProps<FieldProps & {
    options?: string[]
    componentField: any
    disabled: boolean | undefined
}>()
</script>

<template>
    <Select :disabled="disabled" v-bind="{ ...componentField }">
        <SelectTrigger class="w-full">
            <SelectValue :placeholder="config?.inputProps?.placeholder" />
        </SelectTrigger>
        <SelectContent>
            <SelectItem v-for="option in options" :key="option" :value="option">
                {{ beautifyObjectName(option) }}
            </SelectItem>
        </SelectContent>
    </Select>
</template>
