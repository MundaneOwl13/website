<!-- src/routes/+page.svelte -->
<!-- The main page — Hero, Work (photo gallery), About, Contact -->

<script>
  // ============================================================
  // PHOTO DATA
  // Drop your photos into: static/portfolio/
  // Update the src and caption for each photo below.
  // e.g. src: '/portfolio/my-shot.jpg'
  // ============================================================
  const photos = [
    {
      id: 1,
      src: '/portfolio/photo-1.jpg',
      alt: 'Dublin city street at golden hour',
      caption: 'Dublin City Centre — 2024',
    },
    {
      id: 2,
      src: '/portfolio/photo-2.jpg',
      alt: 'Silhouette on a Dublin street',
      caption: 'Grafton Street — 2024',
    },
    {
      id: 3,
      src: '/portfolio/photo-3.jpg',
      alt: 'Rainy evening Dublin',
      caption: 'Temple Bar — 2024',
    },
    {
      id: 4,
      src: '/portfolio/photo-4.jpg',
      alt: 'Morning light Dublin',
      caption: 'Dublin City Centre — 2024',
    },
    {
      id: 5,
      src: '/portfolio/photo-5.jpg',
      alt: 'Architecture and shadow',
      caption: 'Dublin City Centre — 2024',
    },
    {
      id: 6,
      src: '/portfolio/photo-6.jpg',
      alt: 'Street portrait Dublin',
      caption: "O'Connell Street — 2024",
    },
    {
      id: 7,
      src: '/portfolio/photo-7.jpg',
      alt: 'Urban texture',
      caption: 'Portobello — 2024',
    },
    {
      id: 8,
      src: '/portfolio/photo-8.jpg',
      alt: 'Evening commuters',
      caption: 'Dublin City Centre — 2024',
    },
  ];

  // ============================================================
  // LIGHTBOX STATE
  // When a photo is clicked, it opens in a fullscreen lightbox.
  // ============================================================
  let lightboxPhoto = $state(null);

  function openLightbox(photo) {
    lightboxPhoto = photo;
    document.body.style.overflow = 'hidden'; // prevent background scroll
  }

  function closeLightbox() {
    lightboxPhoto = null;
    document.body.style.overflow = '';
  }

  // Close lightbox if user presses Escape key
  function handleKeydown(e) {
    if (e.key === 'Escape') closeLightbox();
  }
</script>

<!-- Listen for keyboard events (Escape to close lightbox) -->
<svelte:window onkeydown={handleKeydown} />


<!-- ============================================================
     HERO SECTION
     ============================================================ -->
<section id="hero" class="hero">
  <div class="hero-content">

    <!-- Small label above the headline -->
    <p class="hero-label">Street Photography — Dublin</p>

    <!-- Main headline — the big name -->
    <h1 class="hero-headline">Danish</h1>

    <!-- Sub-headline -->
    <p class="hero-sub">
      Street photographer. Dublin city. Fujifilm X-T5.
    </p>

    <!-- Scroll hint -->
    <a href="/#work" class="hero-scroll">
      <span>Work</span>
      <span class="hero-scroll-line"></span>
    </a>

  </div>
</section>


<!-- ============================================================
     WORK / GALLERY SECTION
     ============================================================ -->
<section id="work" class="work">

  <p class="section-label">Dublin Streets — 2024</p>

  <!-- Masonry grid — photos sit in a CSS column layout -->
  <div class="masonry-grid">
    {#each photos as photo}
      <!-- Each photo card -->
      <button
        class="photo-card"
        onclick={() => openLightbox(photo)}
        aria-label="View: {photo.alt}"
      >
        <img src={photo.src} alt={photo.alt} loading="lazy" />
        <!-- Caption appears on hover -->
        <div class="photo-caption">{photo.caption}</div>
      </button>
    {/each}
  </div>

</section>


<!-- ============================================================
     ABOUT SECTION
     ============================================================ -->
<section id="about" class="about">

  <p class="section-label">About</p>

  <div class="about-grid">

    <!-- Portrait photo — replace src with your actual photo path -->
    <!-- Put your photo in /static/ and update the src below -->
    <div class="about-portrait">
      <!-- Replace src with your photo. Put it in: static/headshot/ -->
      <img
        src="/headshot/headshot.jpg"
        alt="Danish — portrait"
      />
    </div>

    <!-- Bio text -->
    <div class="about-text">

      <h2 class="about-name">Danish</h2>
      <p class="about-tagline">Dublin. Street. Light.</p>

      <p>
        Based in Dublin. Final-year Business Information Systems student at
        Dublin Business School by day & street photographer whenever the light is good.
      </p>
      <p>
        I shoot with a Fujifilm X-T5, mostly around Dublin city centre, drawn to
        golden-hour raking light, silhouettes, and the quiet moments people don't notice.
      </p>
      <p>
        Professionally I work with data: Power BI, Tableau, Excel, SQL.
      </p>

      <!-- Fun facts / camera details -->
      <ul class="about-facts">
        <li>Fujifilm X-T5 &nbsp;·&nbsp; XF 16–50mm &nbsp;·&nbsp; Classic Neg</li>
        <li>Available light only — no flash, no studio</li>
        <li>Final year BIS, Dublin Business School</li>
      </ul>

    </div>

  </div>

</section>


<!-- ============================================================
     CONTACT SECTION
     ============================================================ -->
<section id="contact" class="contact">

  <p class="section-label">Contact</p>

  <div class="contact-content">
    <h2 class="contact-headline">Get in touch</h2>
    <p class="contact-sub">
      For commissions, collaborations, or just to talk photography.
    </p>

    <!-- Replace with your actual email address -->
    <a href="mailto:your@email.com" class="contact-email">
      uwais1307@email.com
    </a>
  </div>

</section>


<!-- ============================================================
     LIGHTBOX OVERLAY
     Shows a photo fullscreen when clicked.
     ============================================================ -->
{#if lightboxPhoto}
  <!-- Clicking the backdrop closes the lightbox -->
  <div
    class="lightbox"
    onclick={closeLightbox}
    role="dialog"
    aria-modal="true"
    aria-label="Photo viewer"
  >
    <!-- Stop clicks on the image from closing the lightbox -->
    <div class="lightbox-inner" onclick={(e) => e.stopPropagation()}>
      <img src={lightboxPhoto.src} alt={lightboxPhoto.alt} />
      <p class="lightbox-caption">{lightboxPhoto.caption}</p>
    </div>

    <!-- Close button -->
    <button class="lightbox-close" onclick={closeLightbox} aria-label="Close">✕</button>
  </div>
{/if}


<!-- ============================================================
     STYLES — scoped to this page
     ============================================================ -->
<style>

  /* ---------- HERO ---------- */

  .hero {
    min-height: 100vh;
    display: flex;
    align-items: flex-end;
    padding: 0 60px 80px;
    position: relative;
  }

  /* Subtle grain texture on the hero */
  .hero::before {
    content: '';
    position: absolute;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    opacity: 0.4;
  }

  .hero-content {
    position: relative;
    z-index: 1;
  }

  .hero-label {
    font-size: 9px;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--text-dim);
    margin-bottom: 24px;
    /* Animate in on load */
    animation: fadeUp 1s ease both;
    animation-delay: 0.2s;
  }

  .hero-headline {
    font-family: var(--font-display);
    font-size: clamp(72px, 14vw, 160px);
    font-weight: 300;
    line-height: 0.9;
    letter-spacing: -0.02em;
    color: var(--text-bright);
    animation: fadeUp 1s ease both;
    animation-delay: 0.4s;
  }

  .hero-sub {
    margin-top: 32px;
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--text-dim);
    animation: fadeUp 1s ease both;
    animation-delay: 0.6s;
  }

  .hero-scroll {
    display: inline-flex;
    align-items: center;
    gap: 16px;
    margin-top: 64px;
    font-size: 9px;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--text-dim);
    transition: color 0.3s ease;
    animation: fadeUp 1s ease both;
    animation-delay: 0.8s;
  }

  .hero-scroll:hover {
    color: var(--text-bright);
  }

  .hero-scroll-line {
    display: block;
    width: 40px;
    height: 1px;
    background: currentColor;
    transition: width 0.3s ease;
  }

  .hero-scroll:hover .hero-scroll-line {
    width: 72px;
  }

  /* ---------- WORK / GALLERY ---------- */

  .work {
    padding: 80px 60px;
  }

  /* CSS columns = masonry-like layout */
  .masonry-grid {
    columns: 3;
    column-gap: 8px;
  }

  /* Each photo card */
  .photo-card {
    break-inside: avoid;          /* don't split a photo across columns */
    display: block;
    position: relative;
    margin-bottom: 8px;
    overflow: hidden;
    cursor: pointer;
    background: none;
    border: none;
    padding: 0;
    width: 100%;
  }

  .photo-card img {
    width: 100%;
    height: auto;
    display: block;
    transition: transform 0.5s var(--transition), filter 0.5s ease;
    filter: brightness(0.92);
  }

  .photo-card:hover img {
    transform: scale(1.03);
    filter: brightness(1.05);
  }

  /* Caption that slides up on hover */
  .photo-caption {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 24px 16px 12px;
    font-size: 9px;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: rgba(240, 237, 230, 0.85);
    background: linear-gradient(transparent, rgba(0,0,0,0.6));
    transform: translateY(100%);
    transition: transform 0.35s ease;
  }

  .photo-card:hover .photo-caption {
    transform: translateY(0);
  }

  /* ---------- ABOUT ---------- */

  .about {
    padding: 80px 60px;
  }

  .about-grid {
    display: grid;
    grid-template-columns: 220px 1fr;
    gap: 80px;
    align-items: start;
  }

  /* Portrait image */
  .about-portrait img {
    width: 100%;
    aspect-ratio: 1;
    object-fit: cover;
    object-position: top;
    filter: grayscale(20%) brightness(0.88);
  }

  /* Text column */
  .about-text {
    max-width: 540px;
  }

  .about-name {
    font-family: var(--font-display);
    font-size: 48px;
    font-weight: 300;
    color: var(--text-bright);
    margin-bottom: 4px;
  }

  .about-tagline {
    font-size: 9px;
    letter-spacing: 0.28em;
    text-transform: uppercase;
    color: var(--text-dim);
    margin-bottom: 40px;
  }

  .about-text p {
    color: var(--text);
    margin-bottom: 20px;
    font-size: 13px;
    line-height: 1.9;
  }

  /* Facts list */
  .about-facts {
    list-style: none;
    margin-top: 40px;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .about-facts li {
    font-size: 9px;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--text-dim);
    padding-left: 16px;
    position: relative;
  }

  .about-facts li::before {
    content: '—';
    position: absolute;
    left: 0;
    color: var(--text-dim);
  }

  /* ---------- CONTACT ---------- */

  .contact {
    padding: 80px 60px;
    display: flex;
    flex-direction: column;
  }

  .contact-content {
    max-width: 500px;
  }

  .contact-headline {
    font-family: var(--font-display);
    font-size: 52px;
    font-weight: 300;
    color: var(--text-bright);
    margin-bottom: 16px;
  }

  .contact-sub {
    color: var(--text-dim);
    font-size: 12px;
    margin-bottom: 40px;
  }

  .contact-email {
    font-size: 10px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--text);
    border-bottom: 1px solid var(--text-dim);
    padding-bottom: 4px;
    transition: color 0.3s ease, border-color 0.3s ease;
  }

  .contact-email:hover {
    color: var(--text-bright);
    border-color: var(--text-bright);
  }

  /* ---------- LIGHTBOX ---------- */

  .lightbox {
    position: fixed;
    inset: 0;
    background: rgba(10, 10, 10, 0.96);
    z-index: 200;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: fadeIn 0.25s ease;
  }

  .lightbox-inner {
    max-width: 90vw;
    max-height: 90vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 16px;
  }

  .lightbox-inner img {
    max-width: 90vw;
    max-height: 82vh;
    object-fit: contain;
  }

  .lightbox-caption {
    font-size: 9px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--text-dim);
  }

  .lightbox-close {
    position: fixed;
    top: 28px;
    right: 36px;
    background: none;
    border: none;
    color: var(--text-dim);
    font-size: 18px;
    cursor: pointer;
    transition: color 0.2s ease;
    letter-spacing: 0;
  }

  .lightbox-close:hover {
    color: var(--text-bright);
  }

  /* ---------- ANIMATIONS ---------- */

  @keyframes fadeUp {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
  }

  /* ---------- RESPONSIVE — tablet / mobile ---------- */

  @media (max-width: 900px) {
    .masonry-grid {
      columns: 2;
    }

    .about-grid {
      grid-template-columns: 1fr;
      gap: 40px;
    }

    .about-portrait img {
      max-width: 200px;
    }
  }

  @media (max-width: 600px) {
    section {
      padding: 60px 24px;
    }

    .masonry-grid {
      columns: 1;
    }

    .hero {
      padding: 0 24px 60px;
    }

    .work,
    .about,
    .contact {
      padding: 60px 24px;
    }
  }

</style>
