<script setup lang="ts">
import type { FieldProps } from './interface'
import { Button } from '@/components/ui/button'
import { Calendar } from '@/components/ui/calendar'
import { Popover, PopoverContent, PopoverTrigger } from '@/components/ui/popover'
import { DateFormatter, getLocalTimeZone } from '@internationalized/date'
import { CalendarIcon } from 'lucide-vue-next'
import { cn } from '@/lib/utils'


defineProps<FieldProps & {
  componentField: any
}>()

const df = new DateFormatter('en-US', {
  dateStyle: 'long',
})
</script>

<template>
  <div>
    <Popover>
      <PopoverTrigger as-child :disabled="disabled">
        <Button
          variant="outline"
          :class="cn(
            'w-full justify-start text-left font-normal',
            !(componentField?.modelValue) && 'text-muted-foreground',
          )"
        >
          <CalendarIcon class="mr-2 h-4 w-4" :size="16" />
          {{ 
            componentField?.modelValue 
              ? df.format(componentField.modelValue.toDate(getLocalTimeZone())) 
              : "Pick a date" 
          }}
        </Button>
      </PopoverTrigger>
      <PopoverContent class="w-auto p-0">
        <Calendar initial-focus v-bind="componentField || {}" />
      </PopoverContent>
    </Popover>
  </div>
</template>