<script setup lang="ts">
import type { FieldProps } from './interface'
import { Checkbox } from '@/components/ui/checkbox'
import { FormControl } from '@/components/ui/form'
import { Switch } from '@/components/ui/switch'
import { computed } from 'vue'

const props = defineProps<FieldProps & {
  componentField: any
}>()

const booleanComponent = computed(() => props.config?.component === 'switch' ? Switch : Checkbox)
</script>

<template>
  <div class="space-y-0 mb-3 flex items-center gap-3">
    <component
      :is="booleanComponent"
      v-bind="{ ...componentField }"
      :disabled="disabled"
      :checked="componentField.modelValue"
      @update:checked="componentField['onUpdate:modelValue']"
    />
  </div>
</template>
