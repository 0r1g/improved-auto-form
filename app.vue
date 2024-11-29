<script setup lang="ts">
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import * as z from 'zod'

import { Button } from '@/components/ui/button'
import {
  FormControl,
  FormDescription,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import { Checkbox } from '@/components/ui/checkbox'
import { RadioGroup, RadioGroupItem } from '@/components/ui/radio-group'
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectLabel,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'

const formSchema = toTypedSchema(z.object({
  fullname: z.string().min(2).max(100),
  pronounce: z.enum(['she-her', 'he-him', 'they-them']),
  city: z.enum(['new-york', 'los-angeles', 'chicago', 'miami', 'dallas']),
  username: z.string().min(2).max(50),
  email: z.string().email().min(2).max(50),
  password: z.string().min(6).max(50),
  acceptEmails: z.boolean(),
}));


const form = useForm({
  validationSchema: formSchema,
})

const onSubmit = form.handleSubmit((values) => {
  alert(Object.entries(values).join('\n'))
})
</script>

<template>
  <form class="w-2/3 space-y-6" @submit="onSubmit">
    <!-- Field for entering the full name -->
    <FormField v-slot="{ componentField }" name="fullname">
      <FormItem>
        <FormLabel>Full Name</FormLabel>
        <FormControl>
          <Input type="text" placeholder="Enter your full name" v-bind="componentField" />
        </FormControl>
        <FormDescription>
          This is your complete name.
        </FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>

    <!-- Field for selecting the pronounce -->
    <FormField v-slot="{ componentField }" name="pronounce">
      <FormItem>
        <FormLabel>Pronounce</FormLabel>
        <FormControl>
          <RadioGroup
            class="flex flex-col space-y-1"
            v-bind="componentField"
          >
            <FormItem class="flex items-center space-y-0 gap-x-3">
              <FormControl>
                <RadioGroupItem value="she-her" />
              </FormControl>
              <FormLabel class="font-normal">
                She / Her
              </FormLabel>
            </FormItem>
            <FormItem class="flex items-center space-y-0 gap-x-3">
              <FormControl>
                <RadioGroupItem value="he-him" />
              </FormControl>
              <FormLabel class="font-normal">
                He / Him
              </FormLabel>
            </FormItem>
            <FormItem class="flex items-center space-y-0 gap-x-3">
              <FormControl>
                <RadioGroupItem value="they-them" />
              </FormControl>
              <FormLabel class="font-normal">
                They / Them
              </FormLabel>
            </FormItem>
          </RadioGroup>
        </FormControl>
        <FormDescription>
          Select how you'd like your name to be pronounced.
        </FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>

    <!-- Field for selecting the city -->
    <FormField v-slot="{ componentField }" name="city">
      <FormItem>
        <FormLabel>City</FormLabel>
        <FormControl>
          <Select v-bind="componentField">
            <SelectTrigger class="w-[180px]">
              <SelectValue placeholder="Select a city" />
            </SelectTrigger>
            <SelectContent>
              <SelectGroup>
                <SelectLabel>Cities</SelectLabel>
                <SelectItem value="new-york">
                  New York
                </SelectItem>
                <SelectItem value="los-angeles">
                  Los Angeles
                </SelectItem>
                <SelectItem value="chicago">
                  Chicago
                </SelectItem>
                <SelectItem value="miami">
                  Miami
                </SelectItem>
                <SelectItem value="dallas">
                  Dallas
                </SelectItem>
              </SelectGroup>
            </SelectContent>
          </Select>
        </FormControl>
        <FormDescription>
          Select your city from the list.
        </FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>

    <!-- Field for entering the username -->
    <FormField v-slot="{ componentField }" name="username">
      <FormItem>
        <FormLabel>Username</FormLabel>
        <FormControl>
          <Input type="text" placeholder="Choose a username" v-bind="componentField" />
        </FormControl>
        <FormDescription>
          This is your public display name.
        </FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>

    <!-- Field for entering the email -->
    <FormField v-slot="{ componentField }" name="email">
      <FormItem>
        <FormLabel>Email</FormLabel>
        <FormControl>
          <Input type="email" placeholder="Enter your email" v-bind="componentField" />
        </FormControl>
        <FormDescription>
          This is your email.
        </FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>

    <!-- Field for entering the password -->
    <FormField v-slot="{ componentField }" name="password">
      <FormItem>
        <FormLabel>Password</FormLabel>
        <FormControl>
          <Input type="password" placeholder="Enter your password" v-bind="componentField" />
        </FormControl>
        <FormDescription>
          This is your password.
        </FormDescription>
        <FormMessage />
      </FormItem>
    </FormField>

    <!-- Checkbox for accepting emails -->
    <FormField v-slot="{ value, handleChange }" name="acceptEmails">
      <FormItem>
        <FormControl>
          <Checkbox :checked="value" @update:checked="handleChange" />
        </FormControl>
        <FormLabel>
          I agree to receive emails and updates.
        </FormLabel>
        <FormMessage />
      </FormItem>
    </FormField>

    <!-- Submit Button -->
    <Button type="submit">
      Register
    </Button>
  </form>
</template>

