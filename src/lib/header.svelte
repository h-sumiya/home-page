<script>
  import { elasticOut } from "svelte/easing";
  import { fly, slide } from "svelte/transition";

  let isMenuOpen = false;

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }
</script>

<header class="bg-gray-800 text-white py-4 px-6 shadow-lg">
  <nav class="container mx-auto flex justify-between items-center">
    <a
      href="/"
      class="text-2xl font-bold tracking-tighter transition-colors duration-300 transform hover:scale-105 hover:text-cyan-400"
      >H<span class="text-primary ml-2">Sumiya</span>
    </a>

    <button
      class="md:hidden text-white focus:outline-none"
      on:click={toggleMenu}
      aria-label="Toggle menu"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6 transition-transform duration-300 ease-in-out"
        class:rotate-90={isMenuOpen}
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 6h16M4 12h16m-7 6h7"
        />
      </svg>
    </button>

    <ul class="hidden md:flex space-x-6">
      {#each ["About", "Projects", "Contact"] as item, i}
        <li
          in:fly={{ y: -20, delay: 100 * i, duration: 500, easing: elasticOut }}
        >
          <a href="/{item.toLowerCase()}" class="nav-item">
            <span class="relative z-10">{item}</span>
          </a>
        </li>
      {/each}
    </ul>

    {#if isMenuOpen}
      <div
        class="absolute top-16 left-0 right-0 bg-gray-800 shadow-lg md:hidden"
        transition:slide={{ duration: 300 }}
      >
        <ul class="py-2">
          {#each ["About", "Projects", "Contact"] as item, i}
            <li
              in:fly={{
                x: -50,
                delay: 50 * i,
                duration: 300,
                easing: elasticOut,
              }}
              out:fly={{ x: 50, delay: 50 * i, duration: 300 }}
            >
              <a
                href="/{item.toLowerCase()}"
                class="block py-2 px-4 hover:bg-gray-700 transition-all duration-300 nav-item-mobile"
                on:click={toggleMenu}
              >
                {item}
              </a>
            </li>
          {/each}
        </ul>
      </div>
    {/if}
  </nav>
</header>

<style>
  .rotate-90 {
    transform: rotate(90deg);
  }

  @media (min-width: 768px) {
    .nav-item {
      position: relative;
      overflow: hidden;
    }

    .nav-item::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 2px;
      background-color: var(--color-primary, #00ffff);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.3s ease;
    }

    .nav-item:hover {
      color: var(--color-primary, #00ffff);
    }

    .nav-item:hover::after {
      transform: scaleX(1);
      transform-origin: left;
    }
  }

  @media (max-width: 767px) {
    .nav-item-mobile {
      position: relative;
      transition: all 0.3s ease;
    }

    .nav-item-mobile:active {
      background-color: #374151;
      color: var(--color-primary, #00ffff);
      transform: translateX(10px);
    }

    .nav-item-mobile::before {
      content: "";
      position: absolute;
      left: 0;
      top: 0;
      height: 100%;
      width: 3px;
      background-color: var(--color-primary, #00ffff);
      transform: scaleY(0);
      transition: transform 0.3s ease;
    }

    .nav-item-mobile:active::before {
      transform: scaleY(1);
    }
  }
</style>
