<template>
  <header
    class="py-4 flex gap-4 justify-between items-center px-20 bg-cyan-700"
  >
    <client-only>
      <div class="flex gap-2 items-center">
        Основная валюта:
        <UIDropdown
          :value="currency"
          :response="(value: string) => selectCurrency(value)"
        />
      </div>
    </client-only>
    <nav class="flex gap-4">
      <NuxtLink to="/" active-class="text-gray-400">Главная</NuxtLink>
      <NuxtLink to="/convert" active-class="text-gray-400"
        >Конвертация</NuxtLink
      >
    </nav>
  </header>
</template>

<script setup lang="ts">
const store = useExchangeRate()
const currency = ref<string>("rub")
const selectCurrency = (value: string) => {
  useExchangeRate().current = value
}

onMounted(() => {
  if (store.current) {
    currency.value = store.current
  }
})
</script>
