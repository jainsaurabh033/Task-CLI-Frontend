<script lang="ts">
  import { onMount } from 'svelte';
  import { page } from '$app/stores';

  let currentRoute = '';

  $: currentRoute = $page.url.pathname;
</script>

<div class="layout">
  <aside class="sidebar">
    <div class="logo">TaskCLI</div>
    <nav class="nav">
      <a class:selected={currentRoute === '/dashboard'} href="/dashboard">Dashboard</a>
      <a class:selected={currentRoute === '/tasks'} href="/tasks">Tasks</a>
      <a class:selected={currentRoute === '/profile'} href="/profile">Profile</a>
      <a class:selected={currentRoute === '/manager-analytics'} href="/manager-analytics">Analytics</a>
      <a class:selected={currentRoute === '/public-board'} href="/public-board">Public Board</a>
    </nav>
  </aside>

  <div class="main">
    <header class="topbar">
      <h1>Welcome back 👋</h1>
      <!-- User Info or Logout will go here -->
    </header>

    <main class="content">
      <slot />
    </main>
  </div>
</div>

<style>
  .layout {
    display: flex;
    height: 100vh;
    background-color: var(--bg-color);
    color: var(--text-color);
  }

  .sidebar {
    width: 220px;
    background-color: var(--card-bg);
    padding: 1rem;
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  .logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: var(--primary-color);
  }

  .nav {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .nav a {
    color: var(--text-color);
    text-decoration: none;
    padding: 0.5rem;
    border-radius: var(--border-radius);
    transition: background 0.3s;
  }

  .nav a:hover,
  .nav a[selected="true"] {
    background-color: var(--primary-color);
  }

  .main {
    flex: 1;
    display: flex;
    flex-direction: column;
  }

  .topbar {
    padding: 1rem 2rem;
    background-color: #111827;
    border-bottom: 1px solid #333;
  }

  .topbar h1 {
    margin: 0;
    font-size: 1.2rem;
    color: var(--primary-color);
  }

  .content {
    padding: 2rem;
    overflow-y: auto;
    height: 100%;
  }
</style>
