<script setup lang="ts">
import type { FieldProps } from './interface'
import { FormControl, FormDescription, FormField, FormItem, FormMessage } from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import { Textarea } from '@/components/ui/textarea'
import { computed } from 'vue'
import AutoFormLabel from './AutoFormLabel.vue'
import { beautifyObjectName } from './utils'

const props = defineProps<FieldProps>()
const inputComponent = computed(() => props.config?.component === 'textarea' ? Textarea : Input)
</script>

<template>
  <AutoFormFieldWrapper v-slot="slotProps" :field-name="fieldName" :config="config" :required="required">
    <FormControl>
      <slot v-bind="slotProps">
        <component
          :is="inputComponent"
          type="text"
          v-bind="{ ...slotProps.componentField, ...config?.inputProps }"
          :disabled="disabled"
        />
      </slot>
    </FormControl>
  </AutoFormFieldWrapper>
</template>
