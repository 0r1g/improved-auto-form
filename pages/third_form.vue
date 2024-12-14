<script setup lang="ts">
import { AutoForm } from '@/components/ui/improved-auto-form'
import { Button } from '@/components/ui/button'
import MyComponent from '@/components/MyComponent.vue';
import * as z from 'zod'

const schema = z.object({
    fullname: z.string().min(2).max(100),
    pronounce: z.enum(['she-her', 'he-him', 'they-them']),
    city: z.enum(['new-york', 'los-angeles', 'chicago', 'miami', 'dallas']),
    marshmallows: z.enum(['not many', 'a few', 'a lot', 'too many']),
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
        :field-config="{
            password: {
                label: 'Your secure password',
                inputProps: {
                type: 'password',
                },},
            marshmallows: {
                label: 'How many marshmallows fit in your mouth?',
                component: MyComponent,
                },
        }"
    >

    <Button type="submit">Submit</Button>
    </AutoForm>
</template>