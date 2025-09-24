<script lang="ts">

  import TrendingUpIcon from "@tabler/icons-svelte/icons/trending-up";
  import { Sun, Cloud } from "lucide-svelte";
  import { Badge } from "$lib/components/ui/badge/index.js";
  import * as Card from "$lib/components/ui/card/index.js";
</script>

<div
  class="*:data-[slot=card]:from-primary/5 *:data-[slot=card]:to-card dark:*:data-[slot=card]:bg-card *:data-[slot=card]:shadow-xs flex flex-col sm:flex-row gap-4 px-4 *:data-[slot=card]:bg-gradient-to-t lg:px-6"
>
  <Card.Root class="@container/card flex-1">
    <Card.Header>
      <Card.Description class="text-base">Current Visitors</Card.Description>
      <Card.Title class="@[250px]/card:text-5xl text-4xl font-semibold tabular-nums">
        219
      </Card.Title>
      <Card.Action>
        <Badge variant="outline" class="text-sm">
          <TrendingUpIcon class="w-4 h-4" />
          +12.3%
        </Badge>
      </Card.Action>
    </Card.Header>
    <Card.Footer class="flex-col items-start gap-1.5 text-base">
      <div class="text-muted-foreground">Within park boundaries today</div>
    </Card.Footer>
  </Card.Root>

  <Card.Root class="@container/card flex-1">
    <Card.Header>
      <Card.Description class="text-base">Patrol & Response Teams</Card.Description>
      <Card.Title class="@[250px]/card:text-5xl text-4xl font-semibold tabular-nums">
        1,847
      </Card.Title>
      <Card.Action>
        <Badge variant="outline" class="text-sm">
          <TrendingUpIcon class="w-4 h-4" />
          +8.1%
        </Badge>
      </Card.Action>
    </Card.Header>
    <Card.Footer class="flex-col items-start gap-1.5 text-base">
      <div class="line-clamp-1 flex gap-2 font-medium">
        Active patrol routes <TrendingUpIcon class="size-5" />
      </div>
      <div class="text-muted-foreground">Rangers deployed across zones</div>
    </Card.Footer>
  </Card.Root>

  <Card.Root class="@container/card flex-1">
    <Card.Header>
      <Card.Description class="text-base">Field Conditions</Card.Description>
      <Card.Title class="@[250px]/card:text-5xl text-4xl font-semibold tabular-nums flex items-center gap-3">
        28°C
        <Sun class="w-10 h-10 text-yellow-500" />
      </Card.Title>
      <Card.Action>
        <Badge variant="outline" class="text-sm">
          <Cloud class="w-4 h-4" />
          Optimal
        </Badge>
      </Card.Action>
    </Card.Header>
    <Card.Footer class="flex-col items-start gap-1.5 text-base">
      <div class="line-clamp-1 flex gap-2 font-medium">
        Visibility excellent for operations <Sun class="size-5" />
      </div>
      <div class="text-muted-foreground">Safe conditions for patrol teams</div>
    </Card.Footer>
  </Card.Root>
</div>