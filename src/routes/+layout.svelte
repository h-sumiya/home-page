<script>
  import Footer from "$lib/footer.svelte";
  import Header from "$lib/header.svelte";
  import { fade } from "svelte/transition";
  import "../app.css";
</script>

<div class="flex flex-col min-h-screen bg-gray-900 text-gray-100">
  <Header />
  <main
    class="flex-grow container mx-auto px-4 py-8"
    in:fade={{ duration: 300, delay: 300 }}
  >
    <slot />
  </main>
  <Footer />
</div>
