<script>
  import "../app.css";
</script>

<main class="container">
  <div class="title">Demian Tauri Svelte TODO</div>
  <slot />
</main>

<style lang="scss">
  .container {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    .title {
      margin-top: 40px;
      margin-bottom: 40px;
      font-size: 32px;
      font-weight: bold;
    }
  }
</style>
