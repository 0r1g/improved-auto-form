<script setup lang="ts" generic="U extends ZodAny">
import { defineProps, computed } from 'vue'
import { FormField, FormItem, FormControl, FormDescription, FormMessage } from '@/components/ui/form'
import AutoFormLabel from './AutoFormLabel.vue'
import { beautifyObjectName } from './utils'
import { DEFAULT_ZOD_HANDLERS, INPUT_COMPONENTS } from './constant'
import useDependencies from './dependencies'
import type { ZodAny } from 'zod'
import type { Config, ConfigItem, Shape } from './interface'

const props = defineProps<{
  fieldName: string
  shape: Shape
  config?: any //ConfigItem | Config<U>
}>()

function isValidConfig(config: any): config is ConfigItem {
  return !!config?.component
}

const delegatedProps = computed(() => {
  if (['ZodObject', 'ZodArray'].includes(props.shape?.type))
    return { schema: props.shape?.schema }
  return undefined
})

const { isDisabled, isHidden, isRequired, overrideOptions } = useDependencies(props.fieldName)
</script>

<template>
  <FormField v-slot="slotProps" :name="fieldName">
    <FormItem>
      <AutoFormLabel v-if="!config?.hideLabel" :required="isRequired || shape?.required">
        {{ config?.label || beautifyObjectName(fieldName) || shape?.schema?.description }}
      </AutoFormLabel>
      <FormControl>
        <component
          :is="isValidConfig(config)
            ? typeof config.component === 'string'
              ? INPUT_COMPONENTS[config.component!]
              : config.component
            : INPUT_COMPONENTS[DEFAULT_ZOD_HANDLERS[shape?.type]]"
          v-if="!isHidden"
          :label="shape.schema?.description"
          :required="isRequired || shape.required"
          :options="overrideOptions || shape.options"
          :disabled="isDisabled"
          :config="config"
          :fieldName="fieldName"
          v-bind="slotProps"
        >
          <slot v-bind="slotProps" />
        </component>
      </FormControl>
      <FormDescription v-if="config?.description">
        {{ config.description }}
      </FormDescription>
      <FormMessage />
    </FormItem>
  </FormField>
</template>
