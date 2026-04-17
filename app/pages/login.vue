<script setup lang="ts">
const supabase = useSupabaseClient()
const name = ref('')
const password = ref('')
const loading = ref(false)
const toast = useToast()

const login = async () => {
  if (!name.value || !password.value) return

  loading.value = true
  try {
    const { error } = await supabase.auth.signInWithPassword({
      email: `${name.value.toLowerCase().replace(/\s+/g, '')}@homechat.com`,
      password: password.value
    })

    if (error) {
      console.error('Erro no Login:', error)
      const { error: error2 } = await supabase.auth.signUp({
        email: `${name.value.toLowerCase().replace(/\s+/g, '')}@homechat.com`,
        password: password.value,
        options: {
          data: {
            display_name: name.value
          }
        }
      })

      if (error2) {
        toast.add({
          title: 'Erro no Cadastro',
          description: error2.message,
          color: 'error'
        })
        return
      }

      const { error: error3 } = await supabase.auth.signInWithPassword({
        email: `${name.value.toLowerCase().replace(/\s+/g, '')}@homechat.com`,
        password: password.value
      })

      if (error3) {
        toast.add({
          title: 'Erro no Login',
          description: error3.message,
          color: 'error'
        })
        return
      }
    }

    navigateTo('/chat')
  } finally {
    loading.value = false
  }
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
        <UInput
          v-model="password"
          required
          size="lg"
          name="senha"
          type="password"
          icon="solar:lock-bold-duotone"
          placeholder="Insira sua senha"
        />
        <UButton
          class="rounded-full justify-center"
          size="lg"
          type="submit"
          label="Entrar na conversa"
          icon="solar:dialog-2-bold-duotone"
          :loading="loading"
        />
      </UForm>
    </UPageCard>
  </div>
</template>
