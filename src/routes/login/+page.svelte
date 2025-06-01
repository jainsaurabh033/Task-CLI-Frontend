<script lang="ts">
  import { goto } from "$app/navigation";
  import { loginUser } from "$lib/api/auth";

  let email = '';
  let password = '';

  const handleLogin = async () => {
    try {
      const res = await loginUser({ email, password });
      localStorage.setItem('token', res.token);
      localStorage.setItem('user', JSON.stringify(res.user));
      goto('/dashboard');
    } catch (err:any) {
      alert(err.message || 'Invalid login');
    }
  };
</script>

<div class="login-container">
  <div class="login-box">
    <h1 class="title">TaskCLI Login</h1>

    <!-- svelte-ignore a11y_label_has_associated_control -->
    <label>Email</label>
    <input type="email" bind:value={email} placeholder="you@example.com" />

    <!-- svelte-ignore a11y_label_has_associated_control -->
    <label>Password</label>
    <input type="password" bind:value={password} placeholder="••••••••" />

    <button on:click={handleLogin}>Log In</button>

    <p class="link">
      Don’t have an account? <a href="/register">Register</a>
    </p>
  </div>
</div>

<style>
  .login-container {
    height: 100vh;
    background-color: var(--bg-color);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .login-box {
    background-color: var(--card-bg);
    padding: 2.5rem;
    border-radius: var(--border-radius);
    box-shadow: 0 0 12px rgba(0, 0, 0, 0.3);
    width: 350px;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .title {
    color: var(--primary-color);
    margin-bottom: 1rem;
    text-align: center;
  }

  label {
    font-size: 0.9rem;
    color: var(--text-color);
  }

  input {
    padding: 0.6rem;
    border: 1px solid #444;
    border-radius: var(--border-radius);
    background: #111827;
    color: white;
  }

  button {
    margin-top: 1rem;
    padding: 0.7rem;
    background-color: var(--primary-color);
    color: white;
    border: none;
    border-radius: var(--border-radius);
    cursor: pointer;
  }

  button:hover {
    background-color: #4f46e5;
  }

  .link {
    text-align: center;
    font-size: 0.9rem;
    margin-top: 0.5rem;
  }

  .link a {
    color: var(--primary-color);
    text-decoration: none;
  }
</style>
