<script lang="ts">
  import { PieChart } from "layerchart";
  import TrendingUpIcon from "@lucide/svelte/icons/trending-up";
  import * as Chart from "$lib/components/ui/chart/index.js";
  import * as Card from "$lib/components/ui/card/index.js";

  // Data: Forest officers per zone
  const zoneData = [
    { zone: "Western Range", officers: 50, color: "var(--color-western)" },
    { zone: "Central Range", officers: 70, color: "var(--color-central)" },
    { zone: "Eastern Range", officers: 40, color: "var(--color-eastern)" },
    { zone: "Buffer Zone", officers: 20, color: "var(--color-buffer)" },
  ];

  const zoneConfig = {
    officers: { label: "Officers" },
    western: { label: "Western Range", color: "var(--chart-1)" },
    central: { label: "Central Range", color: "var(--chart-2)" },
    eastern: { label: "Eastern Range", color: "var(--chart-3)" },
    buffer: { label: "Buffer Zone", color: "var(--chart-4)" },
  } satisfies Chart.ChartConfig;

  // Data: Distribution of officials by role
  const roleData = [
    { role: "Police", officers: 60, color: "var(--color-police)" },
    { role: "Forest Rangers", officers: 80, color: "var(--color-rangers)" },
    { role: "Medical Teams", officers: 25, color: "var(--color-medical)" },
    { role: "Incident Responders", officers: 35, color: "var(--color-responders)" },
  ];

  const roleConfig = {
    officers: { label: "Officers" },
    police: { label: "Police", color: "var(--chart-1)" },
    rangers: { label: "Forest Rangers", color: "var(--chart-2)" },
    medical: { label: "Medical Teams", color: "var(--chart-3)" },
    responders: { label: "Incident Responders", color: "var(--chart-4)" },
  } satisfies Chart.ChartConfig;
</script>

<div class="m-6 grid md:grid-cols-2 gap-6">
  <!-- Pie Chart 1: Resource Allocation by Zone -->
  <Card.Root class="flex flex-col">
    <Card.Header class="items-center">
      <Card.Title>Resource Allocation by Zone</Card.Title>
      <Card.Description>Current Deployment of Forest Officials</Card.Description>
    </Card.Header>
    <Card.Content class="flex-1">
      <Chart.Container config={zoneConfig} class="mx-auto aspect-square max-h-[250px]">
        <PieChart
          data={zoneData}
          key="zone"
          value="officers"
          label={(d) =>
            d.zone
              .split(" ")
              .map((word) => word[0].toUpperCase() + word.slice(1))
              .join(" ")}
          cRange={zoneData.map((d) => d.color)}
          props={{ pie: { motion: "tween" } }}
          legend
        >
          {#snippet tooltip()}
            <Chart.Tooltip hideLabel />
          {/snippet}
        </PieChart>
      </Chart.Container>
    </Card.Content>
    <Card.Footer class="flex-col gap-2 text-sm">
      <div class="flex items-center gap-2 font-medium leading-none">
        Allocation updated today <TrendingUpIcon class="size-4" />
      </div>
      <div class="text-muted-foreground leading-none">
        Showing total forest officers assigned per zone
      </div>
    </Card.Footer>
  </Card.Root>

  <!-- Pie Chart 2: Officials by Role -->
  <Card.Root class="flex flex-col">
    <Card.Header class="items-center">
      <Card.Title>Officials Distribution by Role</Card.Title>
      <Card.Description>Current Deployment Across Departments</Card.Description>
    </Card.Header>
    <Card.Content class="flex-1">
      <Chart.Container config={roleConfig} class="mx-auto aspect-square max-h-[250px]">
        <PieChart
          data={roleData}
          key="role"
          value="officers"
          label={(d) =>
            d.role
              .split(" ")
              .map((word) => word[0].toUpperCase() + word.slice(1))
              .join(" ")}
          cRange={roleData.map((d) => d.color)}
          props={{ pie: { motion: "tween" } }}
          legend
        >
          {#snippet tooltip()}
            <Chart.Tooltip hideLabel />
          {/snippet}
        </PieChart>
      </Chart.Container>
    </Card.Content>
    <Card.Footer class="flex-col gap-2 text-sm">
      <div class="flex items-center gap-2 font-medium leading-none">
        Allocation updated today <TrendingUpIcon class="size-4" />
      </div>
      <div class="text-muted-foreground leading-none">
        Showing total officials per role
      </div>
    </Card.Footer>
  </Card.Root>

  
</div>
