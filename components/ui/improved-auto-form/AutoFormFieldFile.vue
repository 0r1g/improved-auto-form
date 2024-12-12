<script setup lang="ts">
import type { FieldProps } from './interface'
import { Button } from '@/components/ui/button'
import { FormControl } from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import { TrashIcon } from 'lucide-vue-next'
import { ref } from 'vue'

defineProps<FieldProps & {
  componentField: any
}>()

const inputFile = ref<File>()
async function parseFileAsString(file: File | undefined): Promise<string> {
  return new Promise((resolve, reject) => {
    if (file) {
      const reader = new FileReader()
      reader.onloadend = () => {
        resolve(reader.result as string)
      }
      reader.onerror = (err) => {
        reject(err)
      }
      reader.readAsDataURL(file)
    }
  })
}
</script>

<template>
  <Input
    v-if="!inputFile"
    type="file"
    v-bind="{ ...config?.inputProps }"
    :disabled="disabled"
    @change="async (ev: InputEvent) => {
      const file = (ev.target as HTMLInputElement).files?.[0]
      inputFile = file
      const parsed = await parseFileAsString(file)
      componentField.onInput(parsed)
    }"
  />
  <div v-else class="flex h-10 w-full items-center justify-between rounded-md border border-input bg-transparent pl-3 pr-1 py-1 text-sm shadow-sm transition-colors">
    <p>{{ inputFile?.name }}</p>
    <Button
      :size="'icon'"
      :variant="'ghost'"
      class="h-[26px] w-[26px]"
      aria-label="Remove file"
      type="button"
      @click="() => {
        inputFile = undefined
        componentField.onInput(undefined)
      }"
    >
      <TrashIcon :size="16" />
    </Button>
  </div>
</template>
