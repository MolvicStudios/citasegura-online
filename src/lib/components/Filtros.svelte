<script lang="ts">
  interface Props {
    categoriaActiva: string;
    ordenAsc: boolean;
    onCategoria: (cat: string) => void;
    onOrden: () => void;
  }

  let { categoriaActiva, ordenAsc, onCategoria, onOrden }: Props = $props();

  const categorias = [
    { valor: 'todas', etiqueta: 'Todas', icono: '🌐' },
    { valor: 'serias', etiqueta: 'Relaciones serias', icono: '💍' },
    { valor: 'casuales', etiqueta: 'Encuentros', icono: '⚡' },
    { valor: 'nicho', etiqueta: 'Nichos', icono: '🎯' }
  ];
</script>

<div class="filtros">
  <div class="filtros-categorias" role="group" aria-label="Filtrar por categoría">
    {#each categorias as cat}
      <button
        class="filtro-btn"
        class:activo={categoriaActiva === cat.valor}
        onclick={() => onCategoria(cat.valor)}
        aria-pressed={categoriaActiva === cat.valor}
      >
        <span class="filtro-icono">{cat.icono}</span>
        {cat.etiqueta}
      </button>
    {/each}
  </div>
  <button class="filtro-orden" onclick={onOrden} aria-label="Cambiar orden">
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
      {#if ordenAsc}
        <path d="M3 8l4-4 4 4M7 4v16M13 16l4 4 4-4M17 20V4" />
      {:else}
        <path d="M3 16l4 4 4-4M7 20V4M13 8l4-4 4 4M17 4v16" />
      {/if}
    </svg>
    Confianza {ordenAsc ? '↑ Asc' : '↓ Desc'}
  </button>
</div>

<style>
  .filtros {
    display: flex;
    flex-wrap: wrap;
    gap: 0.625rem;
    justify-content: center;
    align-items: center;
    margin-bottom: 1.75rem;
  }

  .filtros-categorias {
    display: flex;
    flex-wrap: wrap;
    gap: 0.375rem;
    justify-content: center;
  }

  .filtro-btn {
    display: flex;
    align-items: center;
    gap: 0.375rem;
    padding: 0.5rem 1.125rem;
    border: 2px solid #e2e8f0;
    border-radius: 9999px;
    background: #fff;
    color: #475569;
    font-size: 0.8125rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.18s;
    box-shadow: 0 1px 3px rgba(0,0,0,0.05);
  }

  .filtro-btn:hover {
    border-color: #6366f1;
    color: #6366f1;
    background: #fafafe;
  }

  .filtro-btn.activo {
    background: linear-gradient(135deg, #6366f1, #8b5cf6);
    border-color: transparent;
    color: #fff;
    box-shadow: 0 4px 12px rgba(99, 102, 241, 0.3);
  }

  .filtro-icono {
    font-size: 0.875rem;
  }

  .filtro-orden {
    display: flex;
    align-items: center;
    gap: 0.375rem;
    padding: 0.5rem 1.125rem;
    border: 2px solid #e2e8f0;
    border-radius: 9999px;
    background: #fff;
    color: #334155;
    font-size: 0.8125rem;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.18s;
    box-shadow: 0 1px 3px rgba(0,0,0,0.05);
  }

  .filtro-orden:hover {
    border-color: #6366f1;
    color: #6366f1;
  }

  @media (max-width: 480px) {
    .filtro-btn {
      font-size: 0.75rem;
      padding: 0.4rem 0.875rem;
    }
  }
</style>
