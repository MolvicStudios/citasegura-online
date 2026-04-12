<script lang="ts">
  import { sitios } from '$lib/data/sitios';
  import Buscador from '$lib/components/Buscador.svelte';
  import Filtros from '$lib/components/Filtros.svelte';
  import TarjetaSitio from '$lib/components/TarjetaSitio.svelte';

  let busqueda = $state('');
  let categoriaActiva = $state('todas');
  let ordenAsc = $state(false);

  // Estadísticas globales
  const totalSitios = sitios.length;
  const mediaConfianza = Math.round(sitios.reduce((s, x) => s + x.confianza, 0) / sitios.length);
  const sitiosAlta = sitios.filter((s) => s.confianza >= 80).length;
  const sitiosGratis = sitios.filter((s) => s.modalidad === 'gratuita' || s.modalidad === 'freemium').length;

  let sitiosFiltrados = $derived.by(() => {
    let resultado = sitios.filter((s) => {
      const texto = busqueda.toLowerCase().trim();
      const coincideTexto =
        !texto ||
        s.nombre.toLowerCase().includes(texto) ||
        s.descripcion.toLowerCase().includes(texto) ||
        s.etiquetaCategoria.toLowerCase().includes(texto);
      const coincideCategoria = categoriaActiva === 'todas' || s.categoria === categoriaActiva;
      return coincideTexto && coincideCategoria;
    });
    resultado.sort((a, b) =>
      ordenAsc ? a.confianza - b.confianza : b.confianza - a.confianza
    );
    return resultado;
  });
</script>

<svelte:head>
  <title>CitaSegura.es — Compara sitios de citas en España por confiabilidad</title>
</svelte:head>

<!-- Strip de estadísticas -->
<div class="stats-strip">
  <div class="stat">
    <span class="stat-valor">{totalSitios}</span>
    <span class="stat-label">Plataformas analizadas</span>
  </div>
  <div class="stat-sep" aria-hidden="true"></div>
  <div class="stat">
    <span class="stat-valor">{sitiosAlta}</span>
    <span class="stat-label">Confianza alta (≥80)</span>
  </div>
  <div class="stat-sep" aria-hidden="true"></div>
  <div class="stat">
    <span class="stat-valor">{mediaConfianza}</span>
    <span class="stat-label">Puntuación media</span>
  </div>
  <div class="stat-sep" aria-hidden="true"></div>
  <div class="stat">
    <span class="stat-valor">{sitiosGratis}</span>
    <span class="stat-label">Con acceso gratuito</span>
  </div>
</div>

<!-- Leyenda de colores -->
<div class="leyenda">
  <span class="leyenda-titulo">Índice de confiabilidad:</span>
  <span class="leyenda-item leyenda-alto">● ≥80 Alta</span>
  <span class="leyenda-item leyenda-medio">● 50-79 Media</span>
  <span class="leyenda-item leyenda-bajo">● &lt;50 Baja</span>
</div>

<!-- Buscador -->
<Buscador value={busqueda} onInput={(v) => (busqueda = v)} />

<!-- Filtros -->
<Filtros
  {categoriaActiva}
  {ordenAsc}
  onCategoria={(cat) => (categoriaActiva = cat)}
  onOrden={() => (ordenAsc = !ordenAsc)}
/>

<!-- Resultados -->
{#if sitiosFiltrados.length === 0}
  <div class="sin-resultados">
    <div class="sin-resultados-icono">🔍</div>
    <p>No se encontraron plataformas con esos criterios.</p>
    <button
      class="btn-limpiar"
      onclick={() => { busqueda = ''; categoriaActiva = 'todas'; }}
    >
      Limpiar filtros
    </button>
  </div>
{:else}
  <p class="contador">
    Mostrando <strong>{sitiosFiltrados.length}</strong> de {totalSitios} plataformas
  </p>
  <div class="grid">
    {#each sitiosFiltrados as sitio (sitio.id)}
      <TarjetaSitio {sitio} />
    {/each}
  </div>
{/if}

<style>
  /* Stats strip */
  .stats-strip {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 0;
    background: #fff;
    border: 1px solid #e2e8f0;
    border-radius: 16px;
    padding: 1.25rem 1.5rem;
    margin-bottom: 1.5rem;
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
  }

  .stat {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.125rem;
    padding: 0 1.5rem;
    flex: 1;
    min-width: 100px;
    text-align: center;
  }

  .stat-valor {
    font-size: 2rem;
    font-weight: 900;
    background: linear-gradient(135deg, #4f46e5, #c026d3);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
  }

  .stat-label {
    font-size: 0.75rem;
    color: #64748b;
    font-weight: 500;
  }

  .stat-sep {
    width: 1px;
    height: 40px;
    background: #e2e8f0;
    flex-shrink: 0;
  }

  /* Leyenda */
  .leyenda {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 1.25rem;
    font-size: 0.8125rem;
    color: #64748b;
  }

  .leyenda-titulo {
    font-weight: 600;
    color: #475569;
  }

  .leyenda-alto  { color: #10b981; font-weight: 600; }
  .leyenda-medio { color: #f59e0b; font-weight: 600; }
  .leyenda-bajo  { color: #ef4444; font-weight: 600; }

  /* Contador */
  .contador {
    text-align: center;
    font-size: 0.875rem;
    color: #64748b;
    margin-bottom: 1.25rem;
  }

  /* Grid */
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
    gap: 1.25rem;
  }

  /* Sin resultados */
  .sin-resultados {
    text-align: center;
    padding: 4rem 1rem;
    color: #64748b;
  }

  .sin-resultados-icono {
    font-size: 3rem;
    margin-bottom: 0.75rem;
  }

  .sin-resultados p {
    font-size: 1.0625rem;
    margin-bottom: 1.25rem;
  }

  .btn-limpiar {
    padding: 0.625rem 1.75rem;
    border: 2px solid #6366f1;
    border-radius: 9999px;
    background: transparent;
    color: #6366f1;
    font-size: 0.875rem;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.2s;
  }

  .btn-limpiar:hover {
    background: #6366f1;
    color: #fff;
  }

  @media (max-width: 720px) {
    .grid { grid-template-columns: 1fr; }
    .stat-sep { display: none; }
    .stat { padding: 0.5rem 1rem; }
  }

  @media (max-width: 480px) {
    .stats-strip { gap: 0.5rem; }
  }
</style>
