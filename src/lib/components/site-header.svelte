<script lang="ts">
  import { Button } from "$lib/components/ui/button/index.js";
  import { Separator } from "$lib/components/ui/separator/index.js";
  import { Progress } from "$lib/components/ui/progress/index.js";
  import { Toast } from "$lib/components/ui/toast/index.js";
  import * as Sidebar from "$lib/components/ui/sidebar/index.js";
  import { Sun, Moon, Download } from "lucide-svelte";
  import { onMount } from "svelte";

  let theme: 'light' | 'dark' = 'light';
  let isExporting = false;
  let exportProgress = 0;
  let showToast = false;
  let toastTitle = "";
  let toastDescription = "";

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

  async function handleExport() {
    if (isExporting) return;
    
    isExporting = true;
    exportProgress = 0;
    
    // Simulate progress
    const progressInterval = setInterval(() => {
      exportProgress += Math.random() * 20;
      if (exportProgress >= 100) {
        exportProgress = 100;
        clearInterval(progressInterval);
        performExport();
      }
    }, 100);
  }

  async function performExport() {
    try {
      // Get current timestamp in IST
      const now = new Date();
      const istTime = new Date(now.getTime() + (5.5 * 60 * 60 * 1000)); // Convert to IST (UTC+5:30)
      const timestamp = istTime.toISOString().replace(/[:.]/g, '-').slice(0, 19);
      const filename = `Report_${timestamp}.pdf`;
      
      // Fetch the PDF file
      const response = await fetch('/wtrgp.pdf');
      const blob = await response.blob();
      
      // Create download link
      const url = window.URL.createObjectURL(blob);
      const link = document.createElement('a');
      link.href = url;
      link.download = filename;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
      window.URL.revokeObjectURL(url);
      
      // Show success notification
      toastTitle = "Export Complete";
      toastDescription = `Report saved as ${filename}`;
      showToast = true;
      
      // Auto-hide toast after 3 seconds
      setTimeout(() => {
        showToast = false;
      }, 3000);
      
    } catch (error) {
      console.error('Export failed:', error);
      toastTitle = "Export Failed";
      toastDescription = "Failed to download report";
      showToast = true;
      
      setTimeout(() => {
        showToast = false;
      }, 3000);
    } finally {
      isExporting = false;
      exportProgress = 0;
    }
  }

  function closeToast() {
    showToast = false;
  }
</script>

<header
  class="h-(--header-height) group-has-data-[collapsible=icon]/sidebar-wrapper:h-(--header-height) flex shrink-0 items-center gap-2 border-b transition-[width,height] ease-linear"
>
  <div class="flex w-full items-center gap-1 px-4 lg:gap-2 lg:px-6">
    <Sidebar.Trigger class="-ml-1" />
    <Separator orientation="vertical" class="mx-2 data-[orientation=vertical]:h-4" />
    <h1 class="text-base font-medium">Hazaribagh National Park</h1>
    <div class="ml-auto flex items-center gap-2">
      <Button
        onclick={handleExport}
        variant="ghost"
        size="sm"
        class="flex items-center gap-2 p-1"
        aria-label="Export report"
        disabled={isExporting}
      >
        {#if isExporting}
          <div class="relative h-4 w-4">
            <div class="absolute inset-0 rounded-full border-2 border-gray-300"></div>
            <div 
              class="absolute inset-0 rounded-full border-2 border-blue-500 border-t-transparent animate-spin"
              style="transform: rotate({exportProgress * 3.6}deg)"
            ></div>
          </div>
        {:else}
          <Download class="h-4 w-4" />
        {/if}
        Export
      </Button>
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

<!-- Toast notification -->
<div class="fixed top-4 right-4 z-50">
  <Toast
    show={showToast}
    title={toastTitle}
    description={toastDescription}
    variant="success"
    onClose={closeToast}
  />
</div>

<style>
  :global(svg) {
    transition: color 0.7s;
  }
</style>