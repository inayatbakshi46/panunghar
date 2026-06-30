<script>
  import { onMount } from 'svelte';
  import gsap from 'gsap';

  let isOpen = false;
  let menuContainer;
  let backdrop;
  let menuLinks = [];
  let tl;

  onMount(() => {
    // Initialize GSAP timeline (paused by default)
    tl = gsap.timeline({ paused: true });

    // Animate both the Backdrop and Menu Drawer together
    tl.to(backdrop, {
      duration: 0.4,
      autoAlpha: 1, // Handles both opacity and visibility
      ease: 'power2.out'
    }, 0)
    .to(menuContainer, {
      duration: 0.5,
      x: '0%',
      ease: 'power3.out'
    }, 0)
    // Stagger Menu Links
    .to(menuLinks, {
      duration: 0.4,
      opacity: 1,
      y: 0,
      stagger: 0.08,
      ease: 'power3.out'
    }, '-=0.2');
  });

  function toggleMenu() {
    isOpen = !isOpen;
    if (isOpen) {
      tl.play();
    } else {
      tl.reverse();
    }
  }

  const links = ['Home', 'About', 'Services', 'Contact'];
</script>

<!-- Navbar -->
<nav class="fixed top-0 left-0 right-0 z-30 flex items-center justify-between p-4 bg-white/20 backdrop-blur-md ">
  <div class="text-4xl font-bold font-heading">Panun Ghar</div>

  <!-- Regular Hamburger Button (Triggers Open) -->
  <button 
    on:click={toggleMenu}
    class="flex flex-col justify-between w-8 h-5 focus:outline-none"
    aria-label="Open Menu"
  >
    <span class="w-full h-1 bg-gray-800 rounded"></span>
    <span class="w-full h-1 bg-gray-800 rounded"></span>
    <span class="w-full h-1 bg-gray-800 rounded"></span>
  </button>
</nav>

<!-- Dimmed Backdrop (Clicks here will close the menu) -->
<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div 
  bind:this={backdrop}
  on:click={toggleMenu}
  class="fixed inset-0 z-40 bg-black/50 opacity-0 invisible"
></div>

<!-- Menu Drawer Layout (80% wide on mobile, 45% wide on desktop) -->
<div 
  bind:this={menuContainer}
  class="fixed top-0 bottom-0 left-0 right-auto z-50 w-4/5 md:w-[45%] bg-gray-950 text-white transform -translate-x-full shadow-2xl flex flex-col p-6"
>
  <!-- Header inside drawer containing the Close Button -->
  <div class="flex justify-end w-full mb-12">
    <button 
      on:click={toggleMenu}
      class="relative w-8 h-8 flex items-center justify-center text-gray-400 hover:text-white transition-colors focus:outline-none"
      aria-label="Close Menu"
    >
      <!-- Visual 'X' Button -->
      <span class="absolute w-6 h-0.5 bg-current rotate-45"></span>
      <span class="absolute w-6 h-0.5 bg-current -rotate-45"></span>
    </button>
  </div>

  <!-- Links Container -->
  <ul class="flex flex-col items-center gap-8 text-3xl font-semibold my-auto pb-20">
    {#each links as link, i}
      <li 
        bind:this={menuLinks[i]} 
        class="opacity-0 translate-y-8"
      >
        <a href="#{link.toLowerCase()}" on:click={toggleMenu} class="hover:text-gray-300 transition-colors">
          {link}
        </a>
      </li>
    {/each}
  </ul>
</div>