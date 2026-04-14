<script lang="ts">
  import { onMount } from 'svelte';
  import { browser } from '$app/environment';

  let visible = $state(false);

  function loadAdScripts() {}

  function reject() {
    localStorage.setItem('cookie-consent', 'rejected');
    visible = false;
  }
</script>

{#if visible}
  <div class="cookie-banner" role="dialog" aria-modal="false" aria-label="Aviso de cookies">
    <div class="cookie-inner">
      <div class="cookie-text">
        <strong class="cookie-titulo">🍪 Usamos cookies publicitarias</strong>
        <p>
          Utilizamos cookies de publicidad de terceros (Adsterra) para financiar este servicio
          gratuito. Puedes aceptarlas o rechazarlas. Consulta nuestra
          <a href="/legal/cookies">política de cookies</a>.
        </p>
      </div>
      <div class="cookie-actions">
        <button class="btn-reject" onclick={reject}>Rechazar</button>
        <button class="btn-accept" onclick={accept}>Aceptar todas</button>
      </div>
    </div>
  </div>
{/if}

<style>
  .cookie-banner {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 9999;
    background: #0f172a;
    border-top: 3px solid #6366f1;
    box-shadow: 0 -4px 24px rgba(0, 0, 0, 0.35);
    padding: 1rem 1.25rem;
  }

  .cookie-inner {
    max-width: 1100px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1.5rem;
    flex-wrap: wrap;
  }

  .cookie-text {
    flex: 1;
    min-width: 220px;
  }

  .cookie-titulo {
    display: block;
    color: #e2e8f0;
    font-size: 1rem;
    margin-bottom: 0.3rem;
  }

  .cookie-text p {
    color: #94a3b8;
    font-size: 0.875rem;
    line-height: 1.5;
    margin: 0;
  }

  .cookie-text a {
    color: #818cf8;
    text-decoration: underline;
  }

  .cookie-actions {
    display: flex;
    gap: 0.75rem;
    flex-shrink: 0;
    flex-wrap: wrap;
  }

  .btn-accept,
  .btn-reject {
    padding: 0.6rem 1.25rem;
    border: none;
    border-radius: 8px;
    font-size: 0.9rem;
    font-weight: 600;
    cursor: pointer;
    transition: opacity 0.2s;
  }

  .btn-accept {
    background: #6366f1;
    color: #fff;
  }

  .btn-accept:hover {
    opacity: 0.85;
  }

  .btn-reject {
    background: #1e293b;
    color: #94a3b8;
    border: 1px solid #334155;
  }

  .btn-reject:hover {
    background: #334155;
  }

  @media (max-width: 600px) {
    .cookie-inner {
      flex-direction: column;
      align-items: flex-start;
    }
    .cookie-actions {
      width: 100%;
    }
    .btn-accept,
    .btn-reject {
      flex: 1;
      text-align: center;
    }
  }
</style>
