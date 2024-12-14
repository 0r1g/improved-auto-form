<script setup lang="ts">
import type { FieldProps } from './interface'
import AutoFormFieldEnumRadioGroup from './AutoFormFieldEnumRadioGroup.vue'
import AutoFormFieldEnumSelect from './AutoFormFieldEnumSelect.vue'

const props = defineProps<FieldProps & {
  options?: string[]
  componentField: any
  fieldName: string[]
  config?: any
}>()


// const componentName = props.config?.component || (props.config?.component === 'radio' ? AutoFormFieldEnumRadioGroup : AutoFormFieldEnumSelect)
// const componentName = props.config?.component === 'radio' ? AutoFormFieldEnumRadioGroup : props.config?.component || AutoFormFieldEnumSelect

const componentName = computed(() => {
  if (props.config?.component && props.config?.component !== 'radio' && props.config?.component !== 'select') {
    return props.config?.component
  } else if (props.config?.component === 'radio') {
    return AutoFormFieldEnumRadioGroup
  } else {
    return AutoFormFieldEnumSelect
  }
})
</script>

<template>
  <component
    :is="componentName"
    v-bind="{ options, componentField, disabled, fieldName }"
  />
</template>
