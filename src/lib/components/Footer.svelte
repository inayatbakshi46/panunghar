<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  // Define our column references for GSAP
  let col1, col2, col3;

  onMount(() => {
    // Register the ScrollTrigger plugin inside the browser context
    gsap.registerPlugin(ScrollTrigger);

    // Set initial hidden states instantly
    gsap.set([col1, col2, col3], { opacity: 0, y: 20 });

    // Animate each column cleanly when the footer hits the viewport
    const trigger1 = gsap.to(col1, { opacity: 1, y: 0, duration: 0.6, delay: 0, scrollTrigger: { trigger: col1, start: "top 90%" } });
    const trigger2 = gsap.to(col2, { opacity: 1, y: 0, duration: 0.6, delay: 0.1, scrollTrigger: { trigger: col2, start: "top 90%" } });
    const trigger3 = gsap.to(col3, { opacity: 1, y: 0, duration: 0.6, delay: 0.2, scrollTrigger: { trigger: col3, start: "top 90%" } });

    // Clean up when the user navigates away to prevent memory leaks
    return () => {
      trigger1.scrollTrigger?.kill();
      trigger2.scrollTrigger?.kill();
      trigger3.scrollTrigger?.kill();
      trigger1.kill();
      trigger2.kill();
      trigger3.kill();
    };
  });
</script>

<footer class="w-full flex flex-col md:flex-row md:items-start justify-between items-center gap-12 md:gap-6 p-8 bg-white border-t border-gray-100">
  
  <!-- Column 1: Brand & Socials -->
  <div bind:this={col1} class="flex flex-col items-center gap-3 mx-auto text-center md:items-start md:text-left">
    <h1 class="text-4xl font-bold font-heading text-gray-900">Panun Ghar</h1>
    <div class="flex gap-4 justify-center md:justify-start text-gray-600">
      
      <!-- Instagram Inline SVG -->
      <a href="/" aria-label="Instagram" class="hover:text-pink-600 transition-colors">
        <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <rect width="20" height="20" x="2" y="2" rx="5" ry="5"/>
          <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/>
          <line x1="17.5" x2="17.51" y1="6.5" y2="6.5"/>
        </svg>
      </a>

      <!-- Facebook Inline SVG -->
      <a href="/" aria-label="Facebook" class="hover:text-blue-600 transition-colors">
        <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/>
        </svg>
      </a>

      <!-- Twitter / X Inline SVG -->
      <a href="/" aria-label="Twitter" class="hover:text-black transition-colors">
        <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M22 4s-.7 2.1-2 3.4c1.6 10-9.4 17.3-18 11.6 2.2.1 4.4-.6 6-2C3 15.5.5 9.6 3 5c2.2 2.6 5.6 4.1 9 4-.9-4.2 4-6.6 7-3.8 1.1 0 3-1.2 3-1.2z"/>
        </svg>
      </a>

    </div>
  </div>

  <!-- Column 2: Navigation Links -->
  <div bind:this={col2} class="flex flex-col gap-2 items-center mx-auto text-gray-600 font-medium">
    <a href="/" class="hover:text-gray-900 transition-colors">About</a>
    <a href="/" class="hover:text-gray-900 transition-colors">Contact</a>
    <a href="/" class="hover:text-gray-900 transition-colors">Privacy Policy</a>
  </div>

  <!-- Column 3: Location Details -->
  <div bind:this={col3} class="flex flex-col gap-2 items-center mx-auto text-center md:items-start md:text-left">
    <h1 class="font-bold text-gray-900 uppercase tracking-wider text-xs">Location</h1>
    <p class="text-gray-500 max-w-[200px]">123 Main Street, City, State 12345</p>
  </div>

</footer>