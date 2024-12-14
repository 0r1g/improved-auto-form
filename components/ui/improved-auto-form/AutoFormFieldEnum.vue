<script setup lang="ts">
import type { FieldProps } from './interface'
import AutoFormFieldEnumRadioGroup from './AutoFormFieldEnumRadioGroup.vue'
import AutoFormFieldEnumSelect from './AutoFormFieldEnumSelect.vue'

defineProps<FieldProps & {
  options?: string[]
  componentField: any
  fieldName: string[]
}>()
</script>

<template>
  <AutoFormFieldEnumRadioGroup
    v-if="config?.component === 'radio'"
    :options="options"
    :componentField="componentField"
    :disabled="disabled"
    :fieldName="fieldName"
  />
  <component
    v-else-if="
    config?.component !== undefined && 
    config?.component !== 'select'"
    :is="config?.component"
  />
  <AutoFormFieldEnumSelect
    v-else
    :options="options"
    :componentField="componentField"
    :disabled="disabled"
    :fieldName="fieldName"
  />
</template>
