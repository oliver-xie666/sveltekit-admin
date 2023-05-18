<script>
	import { Bubble, Radar } from 'svelte-chartjs';

	import {
		Chart as ChartJS,
		Title,
		Tooltip,
		Legend,
		PointElement,
		LinearScale,
		RadialLinearScale,
		LineElement
	} from 'chart.js';

	ChartJS.register(
		Title,
		Tooltip,
		Legend,
		PointElement,
		LinearScale,
		RadialLinearScale,
		LineElement
	);

	const bubbleData = {
		labels: 'Bubble',
		datasets: [
			{
				label: 'John',
				data: [
					{
						x: 3,
						y: 7,
						r: 10
					}
				],
				backgroundColor: '#ff6384',
				hoverBackgroundColor: '#ff6384'
			},
			{
				label: 'Peter',
				data: [
					{
						x: 3.2,
						y: 7,
						r: 10
					}
				],
				backgroundColor: '#44e4ee',
				hoverBackgroundColor: '#44e4ee'
			},
			{
				label: 'Donald',
				data: [
					{
						x: 3.4,
						y: 7,
						r: 10
					}
				],
				backgroundColor: '#62088A',
				hoverBackgroundColor: '#62088A'
			}
		]
	};
	const radarData = {
		labels: ['Eating', 'Drinking', 'Sleeping', 'Designing', 'Coding', 'Cycling', 'Running'],
		datasets: [
			{
				label: 'My First dataset',
				backgroundColor: 'rgba(194, 116, 161, 0.5)',
				borderColor: 'rgb(194, 116, 161)',
				data: [65, 59, 90, 81, 56, 55, 40]
			},
			{
				label: 'My Second dataset',
				backgroundColor: 'rgba(71, 225, 167, 0.5)',
				borderColor: 'rgb(71, 225, 167)',
				data: [28, 48, 40, 19, 96, 27, 100]
			}
		]
	};
</script>

<svelte:head>
	<title>Charts</title>
</svelte:head>

<main class="h-full pb-16 overflow-y-auto">
	<div class="container px-6 mx-auto grid">
		<h2 class="my-6 text-2xl font-semibold text-gray-700 dark:text-gray-200">Charts</h2>
		<div>
			<span>Bubble Chart</span>
			<div class="card mt-4">
				<Bubble data={bubbleData} options={{ responsive: true }} />
			</div>
		</div>
		<div>
			<span>Radar Chart</span>
			<div class="card mt-4">
				<Radar data={radarData} options={{ responsive: true }} />
			</div>
		</div>
	</div>
</main>
