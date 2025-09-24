<script lang="ts">
	import * as Chart from "$lib/components/ui/chart/index.js";
	import * as Card from "$lib/components/ui/card/index.js";
	import * as Select from "$lib/components/ui/select/index.js";
	import * as ToggleGroup from "$lib/components/ui/toggle-group/index.js";
	import { scaleUtc } from "d3-scale";
	import { Area, AreaChart } from "layerchart";
	import { curveNatural } from "d3-shape";

	const chartData = [
	  { date: new Date("2024-04-01"), incidents: 5 },
	  { date: new Date("2024-04-02"), incidents: 7 },
	  { date: new Date("2024-04-03"), incidents: 10 },
	  { date: new Date("2024-04-04"), incidents: 12 },
	  { date: new Date("2024-04-05"), incidents: 15 },
	  { date: new Date("2024-04-06"), incidents: 8 },
	  { date: new Date("2024-04-07"), incidents: 6 },
	  { date: new Date("2024-04-08"), incidents: 20 },
	  { date: new Date("2024-04-09"), incidents: 4 },
	  { date: new Date("2024-04-10"), incidents: 25 },
	  { date: new Date("2024-04-11"), incidents: 3 },
	  { date: new Date("2024-04-12"), incidents: 22 },
	  { date: new Date("2024-04-13"), incidents: 5 },
	  { date: new Date("2024-04-14"), incidents: 8 },
	  { date: new Date("2024-04-15"), incidents: 14 },
	  { date: new Date("2024-04-16"), incidents: 6 },
	  { date: new Date("2024-04-17"), incidents: 18 },
	  { date: new Date("2024-04-18"), incidents: 5 },
	  { date: new Date("2024-04-19"), incidents: 7 },
	  { date: new Date("2024-04-20"), incidents: 38 },
	  { date: new Date("2024-04-21"), incidents: 10 },
	  { date: new Date("2024-04-22"), incidents: 6 },
	  { date: new Date("2024-04-23"), incidents: 12 },
	  { date: new Date("2024-04-24"), incidents: 4 },
	  { date: new Date("2024-04-25"), incidents: 8 },
	  { date: new Date("2024-04-26"), incidents: 20 },
	  { date: new Date("2024-04-27"), incidents: 6 },
	  { date: new Date("2024-04-28"), incidents: 5 },
	  { date: new Date("2024-04-29"), incidents: 25 },
	  { date: new Date("2024-04-30"), incidents: 8 },
	  { date: new Date("2024-05-01"), incidents: 7 },
	  { date: new Date("2024-05-02"), incidents: 6 },
	  { date: new Date("2024-05-03"), incidents: 18 },
	  { date: new Date("2024-05-04"), incidents: 5 },
	  { date: new Date("2024-05-05"), incidents: 10 },
	  { date: new Date("2024-05-06"), incidents: 75 },
	  { date: new Date("2024-05-07"), incidents: 8 },
	  { date: new Date("2024-05-08"), incidents: 6 },
	  { date: new Date("2024-05-09"), incidents: 12 },
	  { date: new Date("2024-05-10"), incidents: 4 },
	  { date: new Date("2024-05-11"), incidents: 8 },
	  { date: new Date("2024-05-12"), incidents: 20 },
	  { date: new Date("2024-05-13"), incidents: 5 },
	  { date: new Date("2024-05-14"), incidents: 10 },
	  { date: new Date("2024-05-15"), incidents: 6 },
	  { date: new Date("2024-05-16"), incidents: 75 },
	  { date: new Date("2024-05-17"), incidents: 8 },
	  { date: new Date("2024-05-18"), incidents: 12 },
	  { date: new Date("2024-05-19"), incidents: 6 },
	  { date: new Date("2024-05-20"), incidents: 10 },
	  { date: new Date("2024-05-21"), incidents: 5 },
	  { date: new Date("2024-05-22"), incidents: 20 },
	  { date: new Date("2024-05-23"), incidents: 8 },
	  { date: new Date("2024-05-24"), incidents: 6 },
	  { date: new Date("2024-05-25"), incidents: 52 },
	  { date: new Date("2024-05-26"), incidents: 10 },
	  { date: new Date("2024-05-27"), incidents: 6 },
	  { date: new Date("2024-05-28"), incidents: 8 },
	  { date: new Date("2024-05-29"), incidents: 12 },
	  { date: new Date("2024-05-30"), incidents: 5 },
	  { date: new Date("2024-05-31"), incidents: 20 },
	  { date: new Date("2024-06-01"), incidents: 8 },
	  { date: new Date("2024-06-02"), incidents: 6 },
	  { date: new Date("2024-06-03"), incidents: 75 },
	  { date: new Date("2024-06-04"), incidents: 10 },
	  { date: new Date("2024-06-05"), incidents: 5 },
	  { date: new Date("2024-06-06"), incidents: 12 },
	  { date: new Date("2024-06-07"), incidents: 8 },
	  { date: new Date("2024-06-08"), incidents: 6 },
	  { date: new Date("2024-06-09"), incidents: 10 },
	  { date: new Date("2024-06-10"), incidents: 75 },
	  { date: new Date("2024-06-11"), incidents: 5 },
	  { date: new Date("2024-06-12"), incidents: 12 },
	  { date: new Date("2024-06-13"), incidents: 8 },
	  { date: new Date("2024-06-14"), incidents: 6 },
	  { date: new Date("2024-06-15"), incidents: 10 },
	  { date: new Date("2024-06-16"), incidents: 69 },
	  { date: new Date("2024-06-17"), incidents: 5 },
	  { date: new Date("2024-06-18"), incidents: 12 },
	  { date: new Date("2024-06-19"), incidents: 8 },
	  { date: new Date("2024-06-20"), incidents: 6 },
	  { date: new Date("2024-06-21"), incidents: 10 },
	  { date: new Date("2024-06-22"), incidents: 75 },
	  { date: new Date("2024-06-23"), incidents: 5 },
	  { date: new Date("2024-06-24"), incidents: 12 },
	  { date: new Date("2024-06-25"), incidents: 8 },
	  { date: new Date("2024-06-26"), incidents: 6 },
	  { date: new Date("2024-06-27"), incidents: 10 },
	  { date: new Date("2024-06-28"), incidents: 45 },
	  { date: new Date("2024-06-29"), incidents: 5 },
	  { date: new Date("2024-06-30"), incidents: 12 },
	];

	let timeRange = $state("90d");

	const selectedLabel = $derived.by(() => {
		switch (timeRange) {
			case "90d":
				return "Last 3 months";
			case "30d":
				return "Last 30 days";
			case "7d":
				return "Last 7 days";
			default:
				return "Last 3 months";
		}
	});

	const filteredData = $derived(
		chartData.filter((item) => {
			const referenceDate = new Date("2024-06-30");
			let daysToSubtract = 90;
			if (timeRange === "30d") {
				daysToSubtract = 30;
			} else if (timeRange === "7d") {
				daysToSubtract = 7;
			}

			referenceDate.setDate(referenceDate.getDate() - daysToSubtract);
			return item.date >= referenceDate;
		})
	);

	const incidentsConfig = {
		incidents: { label: "Incidents", color: "var(--primary)" },
	} satisfies Chart.ChartConfig;
</script>

<div class="space-y-6">
	<Card.Root class="@container/card">
		<Card.Header>
			<Card.Title>Incident Trend Analysis</Card.Title>
			<Card.Description>
				<span class="@[540px]/card:block hidden"> Incident Trend Analysis for the last 3 months </span>
				<span class="@[540px]/card:hidden">Last 3 months</span>
			</Card.Description>
			<Card.Action>
				<ToggleGroup.Root
					type="single"
					bind:value={timeRange}
					variant="outline"
					class="@[767px]/card:flex hidden *:data-[slot=toggle-group-item]:!px-4"
				>
					<ToggleGroup.Item value="90d">Last 3 months</ToggleGroup.Item>
					<ToggleGroup.Item value="30d">Last 30 days</ToggleGroup.Item>
					<ToggleGroup.Item value="7d">Last 7 days</ToggleGroup.Item>
				</ToggleGroup.Root>
				<Select.Root type="single" bind:value={timeRange}>
					<Select.Trigger
						size="sm"
						class="**:data-[slot=select-value]:block **:data-[slot=select-value]:truncate @[767px]/card:hidden flex w-40"
						aria-label="Select a value"
					>
						<span data-slot="select-value">
							{selectedLabel}
						</span>
					</Select.Trigger>
					<Select.Content class="rounded-xl">
						<Select.Item value="90d" class="rounded-lg">Last 3 months</Select.Item>
						<Select.Item value="30d" class="rounded-lg">Last 30 days</Select.Item>
						<Select.Item value="7d" class="rounded-lg">Last 7 days</Select.Item>
					</Select.Content>
				</Select.Root>
			</Card.Action>
		</Card.Header>
		<Card.Content class="px-2 pt-4 sm:px-6 sm:pt-6">
			<Chart.Container config={incidentsConfig} class="aspect-auto h-[250px] w-full">
				<AreaChart
					data={filteredData}
					x="date"
					xScale={scaleUtc()}
					series={[
						{
							key: "incidents",
							label: "Incidents",
							color: incidentsConfig.incidents.color,
						},
					]}
					props={{
						area: {
							curve: curveNatural,
							"fill-opacity": 0.4,
							line: { class: "stroke-1" },
							motion: "tween",
						},
						xAxis: {
							ticks: timeRange === "7d" ? 7 : undefined,
							format: (v) => {
								return v.toLocaleDateString("en-US", {
									month: "short",
									day: "numeric",
								});
							},
						},
						yAxis: { format: () => "" },
					}}
				>
					{#snippet marks({ series, getAreaProps })}
						<defs>
							<linearGradient id="fillIncidents" x1="0" y1="0" x2="0" y2="1">
								<stop
									offset="5%"
									stop-color="var(--color-incidents)"
									stop-opacity={1.0}
								/>
								<stop
									offset="95%"
									stop-color="var(--color-incidents)"
									stop-opacity={0.1}
								/>
							</linearGradient>
						</defs>
						{#each series as s, i (s.key)}
							<Area
								{...getAreaProps(s, i)}
								fill="url(#fillIncidents)"
							/>
						{/each}
					{/snippet}
					{#snippet tooltip()}
						<Chart.Tooltip
							labelFormatter={(v: Date) => {
								return v.toLocaleDateString("en-US", {
									month: "short",
									day: "numeric",
								});
							}}
							indicator="line"
						/>
					{/snippet}
				</AreaChart>
			</Chart.Container>
		</Card.Content>
	</Card.Root>
</div>
