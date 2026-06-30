<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';

  let heroSection;
  let title;
  let subtitle;
  let description;
  let ctaButton;

  onMount(() => {
    // 1. We no longer need gsap.set since Tailwind classes handle the initial hidden state.
    
    // 2. Initial Intro Animation (Runs smoothly without any flash of un-styled content)
    gsap.to([title, subtitle, description, ctaButton], {
      opacity: 1,
      x: 0,        // Overrides translate-x-10 and pulls elements back to their true position
      duration: 2,       
      stagger: 0.5,      
      ease: 'power1.out',  
    });
  });
</script>

<main class="min-h-screen my-20">
  <!-- Hero Section Wrapper -->
  <section 
    bind:this={heroSection}
    class="relative w-full h-screen flex items-center justify-start px-6 md:px-16 lg:px-24 bg-cover bg-center overflow-hidden"
    style="background-image: url('src/lib/assets/hero.jpeg');"
  >
    <!-- Vignette / Dark Ambient Overlay to keep text perfectly legible -->
    <div class="absolute inset-0 bg-gradient-to-r from-black/70 via-black/40 to-transparent z-10"></div>
    <div class="absolute inset-0 bg-black/20 z-10"></div>

    <!-- Hero Content Layer -->
    <div class="relative z-20 max-w-3xl flex flex-col items-start gap-4 text-white">
      
      <h1 
        bind:this={title}
        class="text-5xl md:text-7xl lg:text-8xl font-bold font-heading tracking-wide leading-none text-white/95 opacity-0 translate-x-10"
      >
        Panun Ghar
      </h1>

      <h2 
        bind:this={subtitle}
        class="text-xl md:text-2xl font-medium tracking-widest text-gray-300 uppercase mt-1 opacity-0 translate-x-10"
      >
        Experience the Raw Beauty
      </h2>

      <p 
        bind:this={description}
        class="text-base md:text-lg text-gray-300/90 leading-relaxed font-light max-w-xl mt-2 opacity-0 translate-x-10"
      >
        Explore coastal landscapes where rugged mountains meet the infinite sea. 
        Begin your journey into the untouched horizons.
      </p>

      <div bind:this={ctaButton} class="mt-6 opacity-0 translate-x-10">
        <a 
          href="#explore" 
          class="inline-block px-8 py-4 bg-white/90 hover:bg-white text-gray-950 font-medium tracking-wider uppercase text-sm rounded shadow-lg transition-colors duration-300"
        >
          Start Your Adventure
        </a>
      </div>

    </div>
  </section>
</main>