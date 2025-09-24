<script lang="ts">
  import { Button } from "$lib/components/ui/button/index.js";
  import { Separator } from "$lib/components/ui/separator/index.js";
  import * as Sidebar from "$lib/components/ui/sidebar/index.js";
  import { Sun, Moon } from "lucide-svelte";
  import { onMount } from "svelte";

  let theme: 'light' | 'dark' = 'light';

  onMount(() => {
    const savedTheme = localStorage.getItem('theme');
    if (savedTheme === 'dark' || savedTheme === 'light') {
      theme = savedTheme as 'light' | 'dark';
      document.documentElement.classList.toggle('dark', theme === 'dark');
    } else {
      const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
      theme = prefersDark ? 'dark' : 'light';
      document.documentElement.classList.toggle('dark', prefersDark);
    }
  });

  function toggleTheme() {
    theme = theme === 'light' ? 'dark' : 'light';
    document.documentElement.classList.toggle('dark', theme === 'dark');
    localStorage.setItem('theme', theme);
  }

  // Handle click with proper typing
  const handleToggleClick = () => {
    toggleTheme();
  };
</script>

<header
  class="h-(--header-height) group-has-data-[collapsible=icon]/sidebar-wrapper:h-(--header-height) flex shrink-0 items-center gap-2 border-b transition-[width,height] ease-linear"
>
  <div class="flex w-full items-center gap-1 px-4 lg:gap-2 lg:px-6">
    <Sidebar.Trigger class="-ml-1" />
    <Separator orientation="vertical" class="mx-2 data-[orientation=vertical]:h-4" />
    <h1 class="text-base font-medium">Kaziranga National Park</h1>
    <div class="ml-auto flex items-center gap-2">
      <Button
        onclick={handleToggleClick}
        variant="ghost"
        size="sm"
        class="flex items-center gap-2 p-1"
        aria-label="Toggle light/dark mode"
      >
        {#if theme === 'light'}
          <Sun class="text-yellow-500" />
        {:else}
          <Moon class="text-blue-400" />
        {/if}
      </Button>
    </div>
  </div>
</header>

<style>
  :global(svg) {
    transition: color 0.7s;
  }
</style>