<script setup lang="ts">
import type { FieldProps } from './interface'
import { FormControl, FormDescription, FormField, FormItem, FormMessage } from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import AutoFormLabel from './AutoFormLabel.vue'
import { beautifyObjectName } from './utils'

defineOptions({
  inheritAttrs: false,
})

defineProps<FieldProps>()
</script>

<template>
  <AutoFormFieldWrapper v-slot="slotProps" :field-name="fieldName" :config="config" :required="required">
    <FormControl>
        <slot v-bind="slotProps">
          <Input type="number" v-bind="{ ...slotProps.componentField, ...config?.inputProps }" :disabled="disabled" />
        </slot>
      </FormControl>
  </AutoFormFieldWrapper>
</template>
