<script lang="ts">
	import { closeSideMenu, pageMenus, togglePageMenu } from '$stores/menus';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';

	const appName = import.meta.env.VITE_APP_NAME;

	$: changeLink = (link: any) => {
		closeSideMenu();
		goto(link.url);
	};

	$: isMainLink = (link: any) => {
		if (!link.url) {
			return false;
		}
		return link.url === activeUrl.pathname;
	};

	$: isChildLink = (link: any) => {
		if (!link.url) {
			return false;
		}
		return activeUrl.pathname.indexOf(link.url, 0) >= 0;
	};

	$: activeUrl = $page.url;

	export let withTitle = true;
	export let links = [
		{
			name: 'Dashboard',
			url: '/',
			icon: 'fa-house'
		},
		{
			name: 'Forms',
			url: '/forms',
			icon: 'fa-list'
		},
		{
			name: 'Cards',
			url: '/cards',
			icon: 'fa-magnet'
		},
		{
			name: 'Charts',
			url: '/charts',
			icon: 'fa-hashtag'
		},
		{
			name: 'Buttons',
			url: '/buttons',
			icon: 'fa-arrow-pointer'
		},
		{
			name: 'Codes',
			url: '/codes',
			icon: 'fa-code'
		},
		{ name: 'Tables', url: '/tables', icon: ' fa-table' },
		{
			name: 'Pages',
			url: '/pages',
			icon: 'fa-folder',
			sublinks: [
				{ name: 'Login', url: '/login' },
				{ name: 'Register', url: '/register' },
				{ name: '404', url: '/this-page-does-not-exists-at-all' }
			]
		}
	];
</script>

<div class="py-4 text-gray-500 dark:text-gray-400 w-64 bg-surface-100-800-token h-screen">
	{#if withTitle}
		<a class="ml-6 text-lg font-bold text-gray-800 dark:text-gray-200" href="/">{appName}</a>
	{/if}
	<ul class="mt-6">
		{#each links as link, a}
			<li class="relative px-6 py-3">
				{#if isMainLink(link)}
					<span
						class="absolute inset-y-0 left-0 w-1 variant-filled-primary rounded-tr-lg rounded-br-lg"
						aria-hidden="true"
					/>
				{/if}

				{#if !link.sublinks}
					<a
						class="{isMainLink(link) &&
							'text-gray-800 dark:text-gray-100'} inline-flex items-center w-full text-sm font-semibold transition-colors duration-150 hover:text-gray-800 dark:hover:text-gray-200"
						href={link.url}
						on:click={(e) => {
							e.preventDefault();
							changeLink(link);
						}}
					>
						{#if link.icon}
							<i class="fa-regular {link.icon}" />
						{/if}
						<span class="ml-4">{link.name}</span>
					</a>
				{:else}
					<button
						on:click={() => togglePageMenu(link.name)}
						class="{isChildLink(link) &&
							'text-gray-800 dark:text-gray-100'} inline-flex items-center justify-between w-full text-sm font-semibold transition-colors duration-150 hover:text-gray-800 dark:hover:text-gray-200"
						aria-haspopup="true"
					>
						<span class="inline-flex items-center">
							{#if link.icon}
								<i class="fa-regular {link.icon}" />
							{/if}
							<span class="ml-4">{link.name}</span>
						</span>
						<svg class="w-4 h-4" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20">
							<path
								fill-rule="evenodd"
								d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
								clip-rule="evenodd"
							/>
						</svg>
					</button>
					{#if $pageMenus[link.name] || isChildLink(link)}
						<ul
							class="p-2 mt-2 space-y-2 overflow-hidden text-sm font-medium text-gray-500 rounded-md shadow-inner bg-gray-50 dark:text-gray-400 dark:bg-gray-900"
							aria-label="submenu"
						>
							{#each link.sublinks as sublink, c}
								<li
									class="relative px-2 py-1 transition-colors duration-150 hover:text-gray-800 dark:hover:text-gray-200"
								>
									{#if isMainLink(sublink)}
										<span
											class="absolute inset-y-0 left-0 w-1 variant-filled-primary rounded-tr-lg rounded-br-lg"
											aria-hidden="true"
										/>
									{/if}
									<a class="w-full" href={sublink.url}>{sublink.name}</a>
								</li>
							{/each}
						</ul>
					{/if}
				{/if}
			</li>
		{/each}
	</ul>
</div>
