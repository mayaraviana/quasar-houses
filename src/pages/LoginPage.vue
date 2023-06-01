<template>
  <q-page>
    <q-layout>
      <q-layout-header class="row">
        <!-- Primeira coluna -->
        <div class="column q-pa-sm">
          <div class="content">
            <h1>
              Welcome to <span class="orange">Search and Stay</span>,<br />
              A Happier way to find your perfect destination!
            </h1>
            <p>
              Discover the key to a happier holiday with our curated selection
              of accommodations.
            </p>
            <!-- Formulário de login -->
            <form class="login-form" @submit="login">
              <div class="form-group q-mb-md">
                <label for="email">Email</label>
                <input
                  type="email"
                  id="email"
                  placeholder="Digite seu email"
                  v-model="email"
                />
              </div>
              <div class="form-group q-mb-sm">
                <label for="password">Senha</label>
                <input
                  type="password"
                  id="password"
                  placeholder="Digite sua senha"
                  v-model="password"
                />
              </div>
              <div class="form-group forgot-password q-mb-md">
                <a href="#">Esqueceu sua senha?</a>
              </div>
              <div class="form-group q-mb-sm">
                <q-btn
                  unelevated
                  color="primary"
                  text-color="white"
                  label="Login"
                  class="login-button"
                  type="submit"
                />
              </div>
              <div class="form-group">
                <q-btn
                  unelevated
                  color="secondary"
                  text-color="black"
                  label="Precisa de uma conta? Cadastre-se"
                  class="login-button"
                  type="button"
                />
              </div>
            </form>
          </div>
        </div>

        <!-- Segunda coluna -->
        <div class="column md">
          <div class="image-container">
            <!-- Imagem que preenche metade da tela -->
            <img
              src="./../assets/Section.png"
              alt="Imagem"
              class="full-image"
            />
          </div>
        </div>
      </q-layout-header>
    </q-layout>
  </q-page>
</template>

<script>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

export default {
  setup() {
    const email = ref('');
    const password = ref('');

    const router = useRouter();

    const login = (event) => {
      event.preventDefault();

      // Access the TOKEN environment variable
      const token = process.env.VITE_TOKEN;

      // Perform login logic here
      localStorage.setItem('token', token);
      // Redirect to HousesPage
      router.push('/houses');
    };

    return {
      email,
      password,
      login,
    };
  },
};
</script>
<style lang="scss" scoped>
h1 {
  font-weight: 600;
  font-size: 1.75rem;
  line-height: 150%;
  color: #101828;
}
.column {
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.orange {
  color: #fb3b11;
}
.content {
  padding-top: 3rem;
  width: 25rem;
}
.full-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
p {
  font-size: 1rem;
  line-height: 24px;
  color: #667085;
}
.login-button {
  width: 100%;
}

.login-form {
  .form-group {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
  }
  label {
    font-weight: 500;
    font-size: 14px;
    line-height: 20px;
  }
  input {
    background: #ffffff;
    border: 1px solid #d0d5dd;
    box-shadow: 0px 1px 2px rgba(16, 24, 40, 0.05);
    border-radius: 8px;
    padding: 0.5rem;
  }
}
</style>
