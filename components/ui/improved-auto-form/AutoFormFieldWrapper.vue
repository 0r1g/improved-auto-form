<!-- AutoFormFieldWrapper.vue -->
<template>
  <FormField v-slot="slotProps" :name="fieldName">
    <FormItem>
      <AutoFormLabel v-if="!config?.hideLabel" :required="required">
        {{ config?.label || beautifyObjectName(label ?? fieldName) }}
      </AutoFormLabel>
      <FormControl>
        <slot v-bind="slotProps" />
      </FormControl>
      <FormDescription v-if="config?.description">
        {{ config.description }}
      </FormDescription>
      <FormMessage />
    </FormItem>
  </FormField>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
import { FormField, FormItem, FormControl, FormDescription, FormMessage } from '@/components/ui/form'
import AutoFormLabel from './AutoFormLabel.vue'
import type { Config, ConfigItem } from './interface'
import { beautifyObjectName } from './utils'

const props = defineProps<{
  fieldName: string
  config?: any
  required?: boolean
  label?: string
}>()
</script>