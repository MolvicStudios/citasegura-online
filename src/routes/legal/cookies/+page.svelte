<svelte:head>
  <title>Política de Cookies - CitaSegura.online</title>
</svelte:head>

<article class="legal">
  <h1>Política de Cookies</h1>

  <section>
    <h2>¿Qué son las cookies?</h2>
    <p>
      Las cookies son pequeños archivos de texto que los sitios web almacenan en el dispositivo del
      usuario (ordenador, teléfono móvil, tableta) cuando se navega por internet. Sirven para
      recordar información sobre la visita, como preferencias de idioma y otras opciones.
    </p>
  </section>

  <section>
    <h2>¿Qué cookies utiliza este sitio?</h2>
    <p>
      <strong>CitaSegura.online</strong> utiliza cookies de publicidad de terceros a través de
      <strong>Adsterra</strong> para financiar el mantenimiento de este servicio gratuito.
      Estas cookies solo se activan si el usuario acepta expresamente su uso a través del banner
      de consentimiento que aparece al acceder al sitio.
    </p>
    <p>
      Las cookies de Adsterra pueden incluir cookies de seguimiento publicitario y perfilado de
      interés. Los dominios desde los que se sirven los anuncios pueden variar (red rotativa).
    </p>
    <table class="cookie-tabla">
      <thead>
        <tr><th>Proveedor</th><th>Finalidad</th><th>Tipo</th><th>Duración</th></tr>
      </thead>
      <tbody>
        <tr>
          <td>Adsterra</td>
          <td>Publicidad y monetización</td>
          <td>Terceros</td>
          <td>Sesión / hasta 1 año</td>
        </tr>
        <tr>
          <td>CitaSegura.online</td>
          <td>Guardar preferencia de consentimiento de cookies</td>
          <td>Propia (localStorage)</td>
          <td>Persistente</td>
        </tr>
      </tbody>
    </table>
  </section>

  <section>
    <h2>Consentimiento y retirada</h2>
    <p>
      Al entrar en el sitio se muestra un banner de cookies. Si acepta, las cookies publicitarias
      se cargarán durante la sesión. Su decisión queda guardada en <code>localStorage</code>
      bajo la clave <code>cookie-consent</code>. Para retirar el consentimiento, borre los datos
      del sitio en su navegador o contacte con nosotros.
    </p>
  </section>

  <section>
    <h2>Cómo gestionar las cookies</h2>
    <p>
      Puede configurar su navegador para bloquear o eliminar cookies. A continuación puede consultar
      cómo hacerlo en los navegadores más comunes:
    </p>
    <ul>
      <li><strong>Chrome:</strong> Configuración → Privacidad y seguridad → Cookies</li>
      <li><strong>Firefox:</strong> Opciones → Privacidad y seguridad → Cookies</li>
      <li><strong>Safari:</strong> Preferencias → Privacidad → Cookies</li>
      <li><strong>Edge:</strong> Configuración → Cookies y permisos del sitio</li>
    </ul>
  </section>

  <section>
    <h2>Base legal</h2>
    <p>
      Esta política de cookies se rige por la normativa española y europea aplicable:
    </p>
    <ul>
      <li>Ley 34/2002 (LSSI-CE), artículo 22.2.</li>
      <li>Reglamento (UE) 2016/679 (RGPD).</li>
      <li>Directrices de la AEPD sobre el uso de cookies.</li>
    </ul>
  </section>

  <a href="/" class="volver">← Volver al inicio</a>
</article>

<style>
  .legal {
    max-width: 720px;
    margin: 0 auto;
    padding: 2rem 0;
  }

  .legal h1 {
    font-size: 2rem;
    color: #1e293b;
    margin-bottom: 1.5rem;
    padding-bottom: 0.75rem;
    border-bottom: 2px solid #e2e8f0;
  }

  .legal h2 {
    font-size: 1.25rem;
    color: #334155;
    margin-top: 1.5rem;
    margin-bottom: 0.5rem;
  }

  .legal p, .legal li {
    color: #475569;
    line-height: 1.7;
    font-size: 0.9375rem;
  }

  .legal ul {
    padding-left: 1.5rem;
    margin-top: 0.5rem;
  }

  .legal li {
    margin-bottom: 0.25rem;
  }

  .volver {
    display: inline-block;
    margin-top: 2rem;
    color: #6366f1;
    text-decoration: none;
    font-weight: 600;
  }

  .volver:hover {
    text-decoration: underline;
  }

  .cookie-tabla {
    width: 100%;
    border-collapse: collapse;
    margin-top: 1rem;
    font-size: 0.875rem;
  }

  .cookie-tabla th,
  .cookie-tabla td {
    border: 1px solid #e2e8f0;
    padding: 0.5rem 0.75rem;
    text-align: left;
    color: #334155;
  }

  .cookie-tabla th {
    background: #f1f5f9;
    font-weight: 600;
  }

  code {
    background: #f1f5f9;
    padding: 0.1em 0.4em;
    border-radius: 4px;
    font-size: 0.85em;
  }
</style>
