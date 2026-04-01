<!-- src/routes/+layout.svelte -->
<!-- This wraps every page — it holds the side nav and imports global styles -->

<script>
  import '../app.css';
  import { page } from '$app/stores';
</script>

<div class="shell">

  <!-- =====================
       SIDE NAVIGATION
       ===================== -->
  <nav class="sidenav">

    <!-- Logo / Name -->
    <a href="/" class="nav-logo">Danish</a>

    <!-- Nav links -->
    <div class="nav-links">
      <a href="/#work"    class:active={$page.url.hash === '#work'}>Work</a>
      <a href="/#about"   class:active={$page.url.hash === '#about'}>About</a>
      <a href="/#contact" class:active={$page.url.hash === '#contact'}>Contact</a>
    </div>

    <!-- Footer info -->
    <div class="nav-footer">
      Dublin<br>
      Fujifilm X-T5<br>
      © {new Date().getFullYear()}
    </div>

  </nav>

  <!-- =====================
       PAGE CONTENT SLOT
       ===================== -->
  <main>
    <slot />
  </main>

</div>
