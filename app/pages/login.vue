<script setup lang="ts">
const supabase = useSupabaseClient()
const name = ref('')
const login = async () => {
  const { error } = await supabase.auth.signInAnonymously({
    options: {
      data: {
        display_name: name.value
      }
    }
  })
  if (error) {
    console.error('Erro no Login Anônimo:', error)
    alert('Falha ao entrar no chat. Verifique se ativou o Login Anônimo no Supabase.')
    return
  }

  navigateTo('/chat')
}
</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-0 h-[calc(100vh-64px)] w-full overflow-hidden">
    <UPageCard
      variant="subtle"
      class="w-sm m-2 py-3"
    >
      <template #title>
        <LogoTexto
          titulo="Login"
          descricao="entre no lar da conversa"
          fota="entrar.png"
        />
      </template>
      <UForm
        class="flex flex-col gap-3"
        @submit="login"
      >
        <UInput
          v-model="name"
          required
          size="lg"
          name="usuario"
          autofocus
          icon="solar:user-bold-duotone"
          placeholder="Insira seu usuário"
        />
        <UButton
          class="rounded-full justify-center"
          size="lg"
          type="submit"
          label="Entrar na conversa"
          icon="solar:dialog-2-bold-duotone"
        />
      </UForm>
    </UPageCard>
  </div>
</template>
