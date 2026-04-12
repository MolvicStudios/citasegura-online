<script lang="ts">
  interface Props {
    value: string;
    onInput: (valor: string) => void;
  }

  let { value, onInput }: Props = $props();
</script>

<div class="buscador">
  <svg class="buscador-icono" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
    <circle cx="11" cy="11" r="8" />
    <path d="m21 21-4.35-4.35" />
  </svg>
  <input
    type="search"
    placeholder="Buscar plataforma por nombre o descripción..."
    {value}
    oninput={(e) => onInput(e.currentTarget.value)}
    class="buscador-input"
    aria-label="Buscar sitios de citas"
  />
  {#if value}
    <button class="buscador-clear" aria-label="Limpiar búsqueda" onclick={() => onInput('')}>✕</button>
  {/if}
</div>

<style>
  .buscador {
    position: relative;
    width: 100%;
    max-width: 640px;
    margin: 0 auto 1.25rem;
  }

  .buscador-icono {
    position: absolute;
    left: 1.125rem;
    top: 50%;
    transform: translateY(-50%);
    width: 1.125rem;
    height: 1.125rem;
    color: #94a3b8;
    pointer-events: none;
  }

  .buscador-input {
    width: 100%;
    padding: 0.9375rem 3rem 0.9375rem 3.125rem;
    border: 2px solid #e2e8f0;
    border-radius: 14px;
    font-size: 1rem;
    background: #fff;
    color: #0f172a;
    transition: border-color 0.2s, box-shadow 0.2s;
    box-sizing: border-box;
    box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  }

  .buscador-input:focus {
    outline: none;
    border-color: #6366f1;
    box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.12), 0 2px 8px rgba(0,0,0,0.05);
  }

  .buscador-input::placeholder {
    color: #94a3b8;
  }

  .buscador-clear {
    position: absolute;
    right: 1rem;
    top: 50%;
    transform: translateY(-50%);
    background: #e2e8f0;
    border: none;
    border-radius: 50%;
    width: 1.5rem;
    height: 1.5rem;
    font-size: 0.6875rem;
    color: #64748b;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background 0.15s;
  }

  .buscador-clear:hover {
    background: #cbd5e1;
    color: #1e293b;
  }
</style>
