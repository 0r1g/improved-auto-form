<script setup lang="ts">
import type { FieldProps } from './interface'
import { FormControl } from '@/components/ui/form'
import { Label } from '@/components/ui/label'
import { RadioGroup, RadioGroupItem } from '@/components/ui/radio-group'
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select'
import AutoFormFieldWrapper from './AutoFormFieldWrapper.vue'
import { beautifyObjectName } from './utils'

defineProps<FieldProps & {
  options?: string[]
}>()
</script>

<template>
  <AutoFormFieldWrapper v-slot="slotProps" :field-name="fieldName" :config="config" :required="required">
    <FormControl>
        <slot v-bind="slotProps">
          <RadioGroup v-if="config?.component === 'radio'" :disabled="disabled" :orientation="'vertical'" v-bind="{ ...slotProps.componentField }">
            <div v-for="(option, index) in options" :key="option" class="mb-2 flex items-center gap-3 space-y-0">
              <RadioGroupItem :id="`${option}-${index}`" :value="option" />
              <Label :for="`${option}-${index}`">{{ beautifyObjectName(option) }}</Label>
            </div>
          </RadioGroup>

          <Select v-else :disabled="disabled" v-bind="{ ...slotProps.componentField }">
            <SelectTrigger class="w-full">
              <SelectValue :placeholder="config?.inputProps?.placeholder" />
            </SelectTrigger>
            <SelectContent>
              <SelectItem v-for="option in options" :key="option" :value="option">
                {{ beautifyObjectName(option) }}
              </SelectItem>
            </SelectContent>
          </Select>
        </slot>
      </FormControl>
  </AutoFormFieldWrapper>
</template>