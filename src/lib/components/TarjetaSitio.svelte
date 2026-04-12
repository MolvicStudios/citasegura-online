<script lang="ts">
  import type { SitioCitas } from '$lib/data/sitios';

  interface Props {
    sitio: SitioCitas;
  }

  let { sitio }: Props = $props();

  const RADIO = 26;
  const CIRCUNFERENCIA = 2 * Math.PI * RADIO; // ≈ 163.36

  function dasharray(valor: number): string {
    return `${(valor / 100) * CIRCUNFERENCIA} ${CIRCUNFERENCIA}`;
  }

  function colorConfianza(v: number): string {
    if (v >= 80) return '#10b981';
    if (v >= 50) return '#f59e0b';
    return '#ef4444';
  }

  function nivelConfianza(v: number): string {
    if (v >= 80) return 'Alta';
    if (v >= 50) return 'Media';
    return 'Baja';
  }

  function antiguedad(anio: number): number {
    return new Date().getFullYear() - anio;
  }

  function etiquetaModalidad(m: string): string {
    if (m === 'gratuita') return 'Gratis';
    if (m === 'premium') return 'Solo premium';
    return 'Freemium';
  }

  function iconoModalidad(m: string): string {
    if (m === 'gratuita') return '🆓';
    if (m === 'premium') return '💳';
    return '⚡';
  }

  function estrellasSvg(puntuacion: number): number[] {
    return [1, 2, 3, 4, 5];
  }

  let mostrarDetalle = $state(false);
</script>

<article class="tarjeta">
  <!-- Banda de color superior según confianza -->
  <div class="tarjeta-banda" style="background: {colorConfianza(sitio.confianza)}"></div>

  <div class="tarjeta-cuerpo">
    <!-- Cabecera: emoji + nombre + gaugeé -->
    <div class="tarjeta-header">
      <div class="tarjeta-identidad">
        <div class="tarjeta-logo">{sitio.logoEmoji}</div>
        <div>
          <div class="tarjeta-nombre-row">
            <h2 class="tarjeta-nombre">{sitio.nombre}</h2>
            {#if sitio.destacado}
              <span class="badge-destacado">⭐ Top</span>
            {/if}
          </div>
          <span class="tarjeta-categoria">{sitio.etiquetaCategoria}</span>
        </div>
      </div>

      <!-- Medidor circular SVG -->
      <div class="gauge-wrap" title="Índice de confiabilidad: {sitio.confianza}/100">
        <svg viewBox="0 0 64 64" width="64" height="64" class="gauge-svg">
          <circle cx="32" cy="32" r={RADIO} fill="none" stroke="#f1f5f9" stroke-width="6" />
          <circle
            cx="32" cy="32" r={RADIO}
            fill="none"
            stroke={colorConfianza(sitio.confianza)}
            stroke-width="6"
            stroke-linecap="round"
            stroke-dasharray={dasharray(sitio.confianza)}
            transform="rotate(-90 32 32)"
          />
          <text x="32" y="37" text-anchor="middle" font-size="14" font-weight="800"
            fill={colorConfianza(sitio.confianza)}>{sitio.confianza}</text>
        </svg>
        <span class="gauge-label" style="color: {colorConfianza(sitio.confianza)}">{nivelConfianza(sitio.confianza)}</span>
      </div>
    </div>

    <!-- Descripción -->
    <p class="tarjeta-desc">{sitio.descripcion}</p>

    <!-- Métricas -->
    <div class="metricas">
      <div class="metrica">
        <span class="metrica-icono">🟢</span>
        <div>
          <span class="metrica-label">Trustpilot</span>
          <span class="metrica-valor">{sitio.trustpilot.toFixed(1)}</span>
          <div class="stars-row">
            {#each estrellasSvg(sitio.trustpilot) as i}
              <span class="star" class:llena={i <= Math.round(sitio.trustpilot)}>★</span>
            {/each}
          </div>
        </div>
      </div>
      <div class="metrica">
        <span class="metrica-icono">📱</span>
        <div>
          <span class="metrica-label">App rating</span>
          <span class="metrica-valor">{sitio.appRating.toFixed(1)}</span>
          <div class="stars-row">
            {#each estrellasSvg(sitio.appRating) as i}
              <span class="star" class:llena={i <= Math.round(sitio.appRating)}>★</span>
            {/each}
          </div>
        </div>
      </div>
      <div class="metrica">
        <span class="metrica-icono">📅</span>
        <div>
          <span class="metrica-label">Antigüedad</span>
          <span class="metrica-valor">{antiguedad(sitio.anioFundacion)} años</span>
          <span class="metrica-sub">Desde {sitio.anioFundacion}</span>
        </div>
      </div>
      <div class="metrica">
        <span class="metrica-icono">👥</span>
        <div>
          <span class="metrica-label">Usuarios ES</span>
          <span class="metrica-valor">{sitio.usuariosEstimados}</span>
        </div>
      </div>
    </div>

    <!-- Badges de características -->
    <div class="badges">
      <span class="badge" class:badge-ok={sitio.gdprCompliant} class:badge-no={!sitio.gdprCompliant}>
        🛡️ {sitio.gdprCompliant ? 'RGPD' : 'Sin RGPD'}
      </span>
      <span class="badge" class:badge-ok={sitio.verificacionPerfil} class:badge-neutral={!sitio.verificacionPerfil}>
        {sitio.verificacionPerfil ? '✅' : '⚠️'} {sitio.verificacionPerfil ? 'Perfil verificado' : 'Sin verificación'}
      </span>
      <span class="badge badge-neutral">
        {iconoModalidad(sitio.modalidad)} {etiquetaModalidad(sitio.modalidad)}
      </span>
      <span class="badge badge-ok">🔒 SSL</span>
    </div>

    <!-- Botones -->
    <div class="tarjeta-acciones">
      <button class="btn-detalle" onclick={() => (mostrarDetalle = !mostrarDetalle)}>
        {mostrarDetalle ? '▲ Ocultar' : '▼ Ver más'}
      </button>
      <a class="btn-visitar" href={sitio.url} target="_blank" rel="noopener noreferrer nofollow">
        Visitar ↗
      </a>
    </div>

    {#if mostrarDetalle}
      <div class="detalle">
        <p>{sitio.descripcionLarga}</p>
      </div>
    {/if}
  </div>
</article>

<style>
  .tarjeta {
    background: #fff;
    border-radius: 18px;
    overflow: hidden;
    box-shadow: 0 2px 12px rgba(0,0,0,0.07);
    transition: transform 0.22s ease, box-shadow 0.22s ease;
    border: 1px solid #e9edf3;
  }

  .tarjeta:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 36px rgba(0,0,0,0.11);
  }

  .tarjeta-banda {
    height: 5px;
    width: 100%;
  }

  .tarjeta-cuerpo {
    padding: 1.25rem 1.375rem 1.375rem;
  }

  /* Header */
  .tarjeta-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 0.75rem;
    margin-bottom: 0.875rem;
  }

  .tarjeta-identidad {
    display: flex;
    align-items: flex-start;
    gap: 0.75rem;
    flex: 1;
  }

  .tarjeta-logo {
    font-size: 2.25rem;
    line-height: 1;
    flex-shrink: 0;
  }

  .tarjeta-nombre-row {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    flex-wrap: wrap;
  }

  .tarjeta-nombre {
    margin: 0;
    font-size: 1.2rem;
    font-weight: 800;
    color: #0f172a;
    letter-spacing: -0.01em;
  }

  .badge-destacado {
    font-size: 0.6875rem;
    font-weight: 700;
    background: linear-gradient(135deg, #f59e0b, #d97706);
    color: #fff;
    padding: 0.125rem 0.5rem;
    border-radius: 9999px;
  }

  .tarjeta-categoria {
    display: inline-block;
    margin-top: 0.25rem;
    font-size: 0.75rem;
    color: #6366f1;
    font-weight: 600;
    background: #eef2ff;
    padding: 0.125rem 0.625rem;
    border-radius: 9999px;
  }

  /* Gauge */
  .gauge-wrap {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.125rem;
    flex-shrink: 0;
  }

  .gauge-svg {
    display: block;
  }

  .gauge-label {
    font-size: 0.65rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  /* Descripción */
  .tarjeta-desc {
    font-size: 0.875rem;
    color: #475569;
    line-height: 1.5;
    margin: 0 0 1rem;
  }

  /* Métricas */
  .metricas {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0.625rem;
    background: #f8fafc;
    border-radius: 12px;
    padding: 0.875rem;
    margin-bottom: 0.875rem;
  }

  .metrica {
    display: flex;
    align-items: flex-start;
    gap: 0.375rem;
  }

  .metrica-icono {
    font-size: 1rem;
    margin-top: 0.1rem;
  }

  .metrica-label {
    display: block;
    font-size: 0.625rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: #94a3b8;
    font-weight: 600;
    line-height: 1;
  }

  .metrica-valor {
    display: block;
    font-size: 0.9rem;
    font-weight: 700;
    color: #1e293b;
    line-height: 1.3;
  }

  .metrica-sub {
    display: block;
    font-size: 0.6875rem;
    color: #94a3b8;
  }

  .stars-row {
    display: flex;
    gap: 1px;
    margin-top: 0.125rem;
  }

  .star {
    font-size: 0.75rem;
    color: #cbd5e1;
    line-height: 1;
  }

  .star.llena {
    color: #f59e0b;
  }

  /* Badges */
  .badges {
    display: flex;
    flex-wrap: wrap;
    gap: 0.375rem;
    margin-bottom: 1rem;
  }

  .badge {
    font-size: 0.6875rem;
    font-weight: 600;
    padding: 0.25rem 0.625rem;
    border-radius: 9999px;
    border: 1px solid;
  }

  .badge-ok {
    background: #f0fdf4;
    color: #15803d;
    border-color: #bbf7d0;
  }

  .badge-no {
    background: #fef2f2;
    color: #dc2626;
    border-color: #fecaca;
  }

  .badge-neutral {
    background: #f1f5f9;
    color: #475569;
    border-color: #e2e8f0;
  }

  /* Acciones */
  .tarjeta-acciones {
    display: flex;
    gap: 0.625rem;
  }

  .btn-detalle,
  .btn-visitar {
    flex: 1;
    padding: 0.625rem 0.875rem;
    border-radius: 10px;
    font-size: 0.8125rem;
    font-weight: 700;
    text-align: center;
    text-decoration: none;
    cursor: pointer;
    transition: all 0.18s;
    border: none;
  }

  .btn-detalle {
    background: #f1f5f9;
    color: #475569;
  }

  .btn-detalle:hover {
    background: #e2e8f0;
  }

  .btn-visitar {
    background: linear-gradient(135deg, #6366f1, #8b5cf6);
    color: #fff;
  }

  .btn-visitar:hover {
    background: linear-gradient(135deg, #4f46e5, #7c3aed);
    transform: translateY(-1px);
  }

  /* Detalle expandible */
  .detalle {
    margin-top: 0.875rem;
    padding: 0.875rem;
    background: #faf5ff;
    border-radius: 10px;
    border-left: 3px solid #8b5cf6;
  }

  .detalle p {
    margin: 0;
    font-size: 0.875rem;
    color: #4c1d95;
    line-height: 1.65;
  }
</style>
