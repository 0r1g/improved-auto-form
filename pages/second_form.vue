<script setup lang="ts">
import { AutoForm, AutoFormField } from '@/components/ui/auto-form'
import { Button } from '@/components/ui/button'
import { h } from 'vue'
import * as z from 'zod'

const schema = z.object({
    fullname: z.string().min(2).max(100),
    pronounce: z.enum(['she-her', 'he-him', 'they-them']),
    city: z.enum(['new-york', 'los-angeles', 'chicago', 'miami', 'dallas']),
    username: z.string().min(2).max(50),
    email: z.string().email().min(2).max(50),
    password: z.string().min(6).max(50),
    acceptEmails: z.boolean().default(false),
})

function onSubmit(values: Record<string, any>) {
    alert(Object.entries(values).join('\n'))
}
</script>

<template>
    <AutoForm
        class="w-2/3 space-y-6"
        :schema="schema"
        @submit="onSubmit"
    >

    <Button type="submit">Submit</Button>
    </AutoForm>
</template>