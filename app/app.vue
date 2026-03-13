<script setup>
useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: '/favicon.png' }
  ],
  htmlAttrs: {
    lang: 'pt-br'
  }
})

const title = 'Home Chat School'
const description = 'O lar da conversa na sua escola!'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  ogImage: '/favicon.png',
  twitterImage: '/favicon.png',
  twitterCard: 'summary_large_image'
})
</script>

<template>
  <UApp>
    <UHeader
      :toggle="false"
    >
      <template #left>
        <NuxtLink
          class="flex items-center gap-2"
          to="/"
        >
          <LogoTexto
            titulo="Home Chat School"
            descricao="Mais um lar da conversa"
            fota="favicon.png"
          />
        </NuxtLink>
      </template>

      <template #right>
        <UColorModeButton />

        <UButton
          v-if="$route.path === '/chat'"
          to="/login"
          icon="solar:logout-3-bold-duotone"
          aria-label="Logout"
          color="neutral"
          variant="ghost"
        />
      </template>
    </UHeader>

    <UMain>
      <NuxtPage />
    </UMain>
  </UApp>
</template>
