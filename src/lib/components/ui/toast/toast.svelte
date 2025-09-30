<script lang="ts">
  import { cn } from "$lib/utils.js";
  import { CheckCircle, X } from "lucide-svelte";

  interface $$Props {
    title?: string;
    description?: string;
    variant?: "default" | "success" | "error";
    class?: string;
    show?: boolean;
    onClose?: () => void;
  }

  let {
    title = "",
    description = "",
    variant = "default",
    class: className,
    show = false,
    onClose,
    ...restProps
  }: $$Props = $props();

  function handleClose() {
    if (onClose) {
      onClose();
    }
  }
</script>

{#if show}
  <div
    class={cn(
      "pointer-events-auto w-full max-w-sm overflow-hidden rounded-lg border bg-background shadow-lg",
      className
    )}
    {...restProps}
  >
    <div class="flex items-start gap-3 p-4">
      {#if variant === "success"}
        <CheckCircle class="h-5 w-5 text-green-500" />
      {:else if variant === "error"}
        <X class="h-5 w-5 text-red-500" />
      {/if}
      <div class="flex-1">
        {#if title}
          <div class="text-sm font-medium">{title}</div>
        {/if}
        {#if description}
          <div class="text-sm text-muted-foreground">{description}</div>
        {/if}
      </div>
      <button
        on:click={handleClose}
        class="text-muted-foreground hover:text-foreground"
      >
        <X class="h-4 w-4" />
      </button>
    </div>
  </div>
{/if}

