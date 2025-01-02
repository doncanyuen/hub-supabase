<script setup>
import { createClient } from "@supabase/supabase-js"
const supabase = createClient(
  "https://xfvndxfvqgkkatldxlnw.supabase.co",
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inhmdm5keGZ2cWdra2F0bGR4bG53Iiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTY3NTY0MTYsImV4cCI6MjAxMjMzMjQxNn0.nY8BhBNPiKFCHbqTrYSgSsxxAYlYqT4MU6lhYtLxtmI"
)
const countries = ref([])

async function getCountries() {
  const { data } = await supabase.from("countries").select()
  countries.value = data
}

onMounted(() => {
  getCountries()
})
</script>

<template>
  <UContainer>
    <UCard class="mt-10">
      <template #header>
        <div class="flex justify-between">
          <h1>Welcome to Nuxt UI Starter</h1>
          <ColorScheme
            ><USelect
              v-model="$colorMode.preference"
              :options="['system', 'light', 'dark']"
          /></ColorScheme>
        </div>
      </template>
      <ul>
        <li v-for="country in countries" :key="country.id">
          {{ country.name }}
        </li>
      </ul>
      <template #footer>
        <UButton
          icon="i-heroicons-book-open"
          to="https://supabase.com/docs/guides/getting-started/quickstarts/nuxtjs"
          target="_blank"
          >Use Supabase with NuxtJS</UButton
        >
      </template>
    </UCard>
  </UContainer>
</template>
