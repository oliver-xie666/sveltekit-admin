<script lang="ts">
	import {
		Avatar,
		ListBox,
		ListBoxItem,
		Paginator,
		Table,
		tableMapperValues
	} from '@skeletonlabs/skeleton';
	import { faker } from '@faker-js/faker';
	import { onMount } from 'svelte';
	import { Line, Bar } from 'svelte-chartjs';

	import {
		Chart as ChartJS,
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		PointElement,
		CategoryScale,
		BarElement
	} from 'chart.js';

	import type { TableSource } from '@skeletonlabs/skeleton';

	const lineData = {
		labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
		datasets: [
			{
				label: 'My First dataset',
				fill: true,
				lineTension: 0.3,
				backgroundColor: 'rgba(225, 204,230, .3)',
				borderColor: 'rgb(205, 130, 158)',
				borderCapStyle: 'butt',
				borderDash: [],
				borderDashOffset: 0.0,
				borderJoinStyle: 'miter',
				pointBorderColor: 'rgb(205, 130,1 58)',
				pointBackgroundColor: 'rgb(255, 255, 255)',
				pointBorderWidth: 10,
				pointHoverRadius: 5,
				pointHoverBackgroundColor: 'rgb(0, 0, 0)',
				pointHoverBorderColor: 'rgba(220, 220, 220,1)',
				pointHoverBorderWidth: 2,
				pointRadius: 1,
				pointHitRadius: 10,
				data: [65, 59, 80, 81, 56, 55, 40]
			},
			{
				label: 'My Second dataset',
				fill: true,
				lineTension: 0.3,
				backgroundColor: 'rgba(184, 185, 210, .3)',
				borderColor: 'rgb(35, 26, 136)',
				borderCapStyle: 'butt',
				borderDash: [],
				borderDashOffset: 0.0,
				borderJoinStyle: 'miter',
				pointBorderColor: 'rgb(35, 26, 136)',
				pointBackgroundColor: 'rgb(255, 255, 255)',
				pointBorderWidth: 10,
				pointHoverRadius: 5,
				pointHoverBackgroundColor: 'rgb(0, 0, 0)',
				pointHoverBorderColor: 'rgba(220, 220, 220, 1)',
				pointHoverBorderWidth: 2,
				pointRadius: 1,
				pointHitRadius: 10,
				data: [28, 48, 40, 19, 86, 27, 90]
			}
		]
	};

	const barData = {
		labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
		datasets: [
			{
				label: '% of Votes',
				data: [12, 19, 3, 5, 2, 3],
				backgroundColor: [
					'rgba(255, 134,159,0.4)',
					'rgba(98,  182, 239,0.4)',
					'rgba(255, 218, 128,0.4)',
					'rgba(113, 205, 205,0.4)',
					'rgba(170, 128, 252,0.4)',
					'rgba(255, 177, 101,0.4)'
				],
				borderWidth: 2,
				borderColor: [
					'rgba(255, 134, 159, 1)',
					'rgba(98,  182, 239, 1)',
					'rgba(255, 218, 128, 1)',
					'rgba(113, 205, 205, 1)',
					'rgba(170, 128, 252, 1)',
					'rgba(255, 177, 101, 1)'
				]
			}
		]
	};

	ChartJS.register(
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		PointElement,
		CategoryScale,
		BarElement
	);

	const sourceData = [
		{ position: 1, name: 'Hydrogen', weight: 1.0079, symbol: 'H' },
		{ position: 2, name: 'Helium', weight: 4.0026, symbol: 'He' },
		{ position: 3, name: 'Lithium', weight: 6.941, symbol: 'Li' },
		{ position: 4, name: 'Beryllium', weight: 9.0122, symbol: 'Be' },
		{ position: 5, name: 'Boron', weight: 10.811, symbol: 'B' }
	];

	const tableSimple: TableSource = {
		// A list of heading labels.
		head: ['Name', 'Symbol', 'Weight'],
		// The data visibly shown in your table body UI.
		body: tableMapperValues(sourceData, ['name', 'symbol', 'weight']),
		// Optional: The data returned when interactive is enabled and a row is clicked.
		meta: tableMapperValues(sourceData, ['position', 'name', 'symbol', 'weight'])
	};

	let page = {
		offset: 0,
		limit: 5,
		size: sourceData.length,
		amounts: [1, 2, 5, 10]
	};

	let currentVariant = 'bg-initial';

	// Types
	interface Person {
		id: number;
		avatar: number;
		name: string;
	}
	interface MessageFeed {
		id: number;
		host: boolean;
		avatar: number;
		name: string;
		timestamp: string;
		message: string;
		color: string;
	}

	let elemChat: HTMLElement;

	const lorem = faker.lorem.paragraph();

	// Navigation List
	const people: Person[] = [
		{ id: 0, avatar: 14, name: 'Michael' },
		{ id: 1, avatar: 40, name: 'Janet' },
		{ id: 2, avatar: 31, name: 'Susan' },
		{ id: 3, avatar: 56, name: 'Joey' },
		{ id: 4, avatar: 24, name: 'Lara' },
		{ id: 5, avatar: 9, name: 'Melissa' }
	];
	let currentPerson: Person = people[0];

	// Messages
	let messageFeed: MessageFeed[] = [
		{
			id: 0,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: 'Yesterday @ 2:30pm',
			message: lorem,
			color: 'variant-soft-primary'
		},
		{
			id: 1,
			host: false,
			avatar: 14,
			name: 'Michael',
			timestamp: 'Yesterday @ 2:45pm',
			message: lorem,
			color: 'variant-soft-primary'
		},
		{
			id: 2,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: 'Yesterday @ 2:50pm',
			message: lorem,
			color: 'variant-soft-primary'
		},
		{
			id: 3,
			host: false,
			avatar: 14,
			name: 'Michael',
			timestamp: 'Yesterday @ 2:52pm',
			message: lorem,
			color: 'variant-soft-primary'
		}
	];
	let currentMessage = '';

	function scrollChatBottom(behavior?: ScrollBehavior): void {
		elemChat.scrollTo({ top: elemChat.scrollHeight, behavior });
	}

	function getCurrentTimestamp(): string {
		return new Date().toLocaleString('en-US', { hour: 'numeric', minute: 'numeric', hour12: true });
	}

	function addMessage(): void {
		const newMessage = {
			id: messageFeed.length,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: `Today @ ${getCurrentTimestamp()}`,
			message: currentMessage,
			color: 'variant-soft-primary'
		};
		// Update the message feed
		messageFeed = [...messageFeed, newMessage];
		// Clear prompt
		currentMessage = '';
		// Smooth scroll to bottom
		// Timeout prevents race condition
		setTimeout(() => {
			scrollChatBottom('smooth');
		}, 0);
	}

	function onPromptKeydown(event: KeyboardEvent): void {
		if (['Enter'].includes(event.code)) {
			event.preventDefault();
			addMessage();
		}
	}

	// When DOM mounted, scroll to bottom
	onMount(() => {
		scrollChatBottom();
	});
</script>

<svelte:head>
	<title>Dashboard</title>
</svelte:head>

<main class="h-full w-full">
	<div class="container px-6 mx-auto grid">
		<h2 class="my-6 text-2xl font-semibold text-gray-700 dark:text-gray-200">Dashboard</h2>
		<!-- -->
		<div class="w-full text-token grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
			<!-- chat -->
			<section class="card">
				<div class="chat w-full h-full grid grid-cols-1 lg:grid-cols-[30%_1fr]">
					<!-- Navigation -->
					<div class="hidden lg:grid grid-rows-[auto_1fr_auto] border-r border-surface-500/30 h-30">
						<!-- Header -->
						<header class="border-b border-surface-500/30 p-4">
							<input class="input" type="search" placeholder="search..." />
						</header>
						<!-- List -->
						<div class="p-4 space-y-4 overflow-y-auto">
							<small class="opacity-50">Contacts</small>
							<ListBox active="variant-filled-primary">
								{#each people as person, i}
									<ListBoxItem bind:group={currentPerson} name="people" value={person}>
										<svelte:fragment slot="lead">
											<Avatar src="https://i.pravatar.cc/?img={person.avatar}" width="w-8" />
										</svelte:fragment>
										{person.name}
									</ListBoxItem>
								{/each}
							</ListBox>
						</div>
					</div>
					<!-- Chart -->
					<div class="grid grid-row-[1fr_auto]">
						<!-- Conversation -->
						<section bind:this={elemChat} class="max-h-[500px] p-4 overflow-y-auto space-y-4">
							{#each messageFeed as bubble, i}
								{#if bubble.host === true}
									<div class="grid grid-cols-[auto_1fr] gap-2">
										<Avatar src="https://i.pravatar.cc/?img={bubble.avatar}" width="w-12" />
										<div class="card p-4 variant-soft rounded-tl-none space-y-2">
											<header class="flex justify-between items-center">
												<p class="font-bold">{bubble.name}</p>
												<small class="opacity-50">{bubble.timestamp}</small>
											</header>
											<p>{bubble.message}</p>
										</div>
									</div>
								{:else}
									<div class="grid grid-cols-[1fr_auto] gap-2">
										<div class="card p-4 rounded-tr-none space-y-2 {bubble.color}">
											<header class="flex justify-between items-center">
												<p class="font-bold">{bubble.name}</p>
												<small class="opacity-50">{bubble.timestamp}</small>
											</header>
											<p>{bubble.message}</p>
										</div>
										<Avatar src="https://i.pravatar.cc/?img={bubble.avatar}" width="w-12" />
									</div>
								{/if}
							{/each}
						</section>
						<!-- Prompt -->
						<section class="border-t border-surface-500/30 p-4">
							<div
								class="input-group input-group-divider grid-cols-[auto_1fr_auto] rounded-container-token"
							>
								<button class="input-group-shim">+</button>
								<textarea
									bind:value={currentMessage}
									class="bg-transparent border-0 ring-0"
									name="prompt"
									id="prompt"
									placeholder="Write a message..."
									rows="1"
									on:keydown={onPromptKeydown}
								/>
								<button
									class={currentMessage ? 'variant-filled-primary' : 'input-group-shim'}
									on:click={addMessage}
								>
									<i class="fa-solid fa-paper-plane" />
								</button>
							</div>
						</section>
					</div>
				</div>
			</section>
			<!-- Card  -->
			<a class="card {currentVariant} card-hover" href="/">
				<header>
					<img
						src="https://source.unsplash.com/vjUokUWbFOs/400x175"
						class="bg-black/50 w-full aspect-[21/9]"
						alt="Post"
					/>
				</header>
				<div class="p-4 space-y-4">
					<h6 class="h6">Announcements</h6>
					<h3 class="h3" data-toc-ignore>Skeleton is Awesome!</h3>
					<article>
						<p>
							<!-- cspell:disable -->
							Lorem ipsum dolor sit amet consectetur adipisicing elit. Numquam aspernatur provident eveniet
							eligendi cumque consequatur tempore sint nisi sapiente. Iste beatae laboriosam iure molestias
							cum expedita architecto itaque quae rem.
							<!-- cspell:enable -->
						</p>
					</article>
				</div>
				<hr class="opacity-50" />
				<footer class="p-4 flex justify-start items-center space-x-4">
					<Avatar src="https://source.unsplash.com/YOErFW8AfkI/32x32" width="w-8" />
					<div class="flex-auto flex justify-between items-center">
						<h6 class="font-bold">By Alex</h6>
						<small>On {new Date().toLocaleDateString()}</small>
					</div>
				</footer>
			</a>
		</div>
		<!-- Table -->
		<Table source={tableSimple} class="mb-2" />
		<Paginator bind:settings={page} />

		<!-- Charts -->
		<h3 class="my-6 text-2xl font-semibold text-gray-700 dark:text-gray-200">Charts</h3>
		<div class="grid gap-6 mb-8 md:grid-cols-2">
			<div class="min-w-0 p-4 rounded-lg shadow-xs dark:bg-gray-800 card">
				<Line data={lineData} options={{ responsive: true }} />
			</div>
			<div class="min-w-0 p-4 rounded-lg shadow-xs dark:bg-gray-800 card">
				<Bar data={barData} options={{ responsive: true }} />
			</div>
		</div>
	</div>
</main>
