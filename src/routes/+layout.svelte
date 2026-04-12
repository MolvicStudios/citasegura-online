<script lang="ts">
  import type { Snippet } from 'svelte';

  interface Props {
    children: Snippet;
  }

  let { children }: Props = $props();
</script>

<svelte:head>
  <title>CitaSegura.es — Compara sitios de citas en España</title>
  <meta name="description" content="Compara los mejores sitios de citas en España por índice de confiabilidad, puntuaciones Trustpilot, app rating y características de seguridad." />
</svelte:head>

<div class="app">
  <header class="header">
    <div class="header-inner">
      <div class="header-top">
        <a href="/" class="logo">
          <div class="logo-shield">🛡️</div>
          <div class="logo-text">
            <span class="logo-nombre">CitaSegura<span class="logo-punto">.es</span></span>
            <span class="logo-tagline">Comparador independiente de plataformas de citas</span>
          </div>
        </a>
        <nav class="header-nav">
          <a href="/legal/aviso-legal">Aviso legal</a>
          <a href="/legal/privacidad">Privacidad</a>
          <a href="/legal/cookies">Cookies</a>
        </nav>
      </div>
    </div>
    <!-- Ola decorativa inferior -->
    <div class="header-wave" aria-hidden="true">
      <svg viewBox="0 0 1440 60" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0,30 C360,60 720,0 1080,30 C1260,45 1380,40 1440,35 L1440,60 L0,60 Z" fill="#f1f5f9"/>
      </svg>
    </div>
  </header>

  <main class="main">
    {@render children()}
  </main>

  <footer class="footer">
    <div class="footer-inner">
      <div class="footer-brand">
        <span class="footer-logo">🛡️ CitaSegura.es</span>
        <p>Proyecto informativo independiente. No afiliado a ninguna plataforma listada.</p>
      </div>
      <nav class="footer-links" aria-label="Páginas legales">
        <a href="/legal/aviso-legal">Aviso legal</a>
        <a href="/legal/privacidad">Política de privacidad</a>
        <a href="/legal/cookies">Política de cookies</a>
      </nav>
      <p class="footer-copy">© {new Date().getFullYear()} CitaSegura.es — Datos orientativos. Las puntuaciones pueden variar.</p>
    </div>
  </footer>
</div>

<style>
  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(body) {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
    background: #f1f5f9;
    color: #0f172a;
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
  }

  .app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  /* ─── Header ─── */
  .header {
    background: linear-gradient(135deg, #312e81 0%, #4f46e5 35%, #7c3aed 65%, #c026d3 100%);
    position: relative;
    padding-bottom: 0;
  }

  .header-inner {
    max-width: 1100px;
    margin: 0 auto;
    padding: 1.5rem 1.25rem 2rem;
  }

  .header-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
    flex-wrap: wrap;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 0.875rem;
    text-decoration: none;
    color: #fff;
  }

  .logo-shield {
    font-size: 2.5rem;
    line-height: 1;
    filter: drop-shadow(0 2px 8px rgba(0,0,0,0.3));
  }

  .logo-nombre {
    display: block;
    font-size: 1.75rem;
    font-weight: 900;
    letter-spacing: -0.03em;
    line-height: 1;
  }

  .logo-punto {
    color: #c4b5fd;
  }

  .logo-tagline {
    display: block;
    font-size: 0.8rem;
    color: #c4b5fd;
    font-weight: 400;
    margin-top: 0.125rem;
  }

  .header-nav {
    display: flex;
    gap: 1.25rem;
  }

  .header-nav a {
    color: #c4b5fd;
    text-decoration: none;
    font-size: 0.8125rem;
    font-weight: 500;
    transition: color 0.2s;
  }

  .header-nav a:hover {
    color: #fff;
  }

  .header-wave {
    width: 100%;
    height: 60px;
    display: block;
  }

  .header-wave svg {
    width: 100%;
    height: 100%;
    display: block;
  }

  /* ─── Main ─── */
  .main {
    flex: 1;
    width: 100%;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 1rem 3rem;
  }

  /* ─── Footer ─── */
  .footer {
    background: #0f172a;
    color: #94a3b8;
    padding: 2rem 1rem;
    text-align: center;
    margin-top: auto;
  }

  .footer-inner {
    max-width: 900px;
    margin: 0 auto;
  }

  .footer-brand {
    margin-bottom: 1rem;
  }

  .footer-logo {
    font-size: 1rem;
    font-weight: 700;
    color: #e2e8f0;
    display: block;
    margin-bottom: 0.25rem;
  }

  .footer-brand p {
    font-size: 0.8125rem;
    color: #64748b;
  }

  .footer-links {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 1.5rem;
    margin-bottom: 1rem;
  }

  .footer-links a {
    color: #94a3b8;
    text-decoration: none;
    font-size: 0.8125rem;
    transition: color 0.2s;
  }

  .footer-links a:hover {
    color: #e2e8f0;
  }

  .footer-copy {
    font-size: 0.75rem;
    color: #475569;
  }

  @media (max-width: 600px) {
    .header-nav { display: none; }
    .logo-nombre { font-size: 1.5rem; }
  }
</style>
