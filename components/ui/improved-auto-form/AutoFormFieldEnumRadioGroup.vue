<script setup lang="ts">
import type { FieldProps } from './interface'
import { Label } from '@/components/ui/label'
import { RadioGroup, RadioGroupItem } from '@/components/ui/radio-group'
import { beautifyObjectName } from './utils'

defineProps<FieldProps & {
    options?: string[]
    componentField: any
    disabled: boolean | undefined
}>()
</script>

<template>
    <RadioGroup :disabled="disabled" :orientation="'vertical'" v-bind="{ ...componentField }">
        <div v-for="(option, index) in options" :key="option" class="mb-2 flex items-center gap-3 space-y-0">
            <RadioGroupItem :id="`${option}-${index}`" :value="option" />
            <Label :for="`${option}-${index}`">{{ beautifyObjectName(option) }}</Label>
        </div>
    </RadioGroup>
</template>
