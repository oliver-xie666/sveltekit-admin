<script lang="ts">
	import {
		toggleProfileMenu,
		closeProfileMenu,
		isProfileMenuOpen,
		toggleSideMenu
	} from '$stores/menus';
	import { AppBar, Avatar, LightSwitch, popup } from '@skeletonlabs/skeleton';
	import { clickOutside } from '$lib/ioevents/click';
	import { keydownEscape } from '$lib/ioevents/keydown';

	const toggleMenu = () => toggleSideMenu();
</script>

<AppBar
	gridColumns="grid-cols-3"
	slotDefault="place-self-center"
	slotTrail="place-content-end"
	shadow="shadow-l"
>
	<svelte:fragment slot="lead">
		<button on:click|stopPropagation|preventDefault={toggleMenu}
			><i class="fa-solid fa-bars text-xl" /></button
		>
	</svelte:fragment>
	<svelte:fragment slot="trail">
		<!-- Theme -->
		<section class="flex justify-between items-center">
			<LightSwitch />
		</section>

		<section class="hidden sm:inline-flex space-x-4">
			<a
				class="btn-icon btn-icon-sm hover:variant-soft-primary"
				href="https://github.com/oliver-xie666/svelte-admin"
				target="_blank"
				rel="noreferrer"
			>
				<i class="fa-brands fa-github text-lg fa-xl" />
			</a>
		</section>
		<div class="relative inline-block">
			<span class="badge-icon variant-filled-error absolute -top-0 right-0.5 z-10 w-2 h-2" />
			<i class="fa-solid fa-bell fa-xl" />
		</div>
		<div class="relative inline-block">
			<div
				on:click={toggleProfileMenu}
				use:keydownEscape
				on:keydown-escape={closeProfileMenu}
				cursor="cursor-pointer"
			>
				<Avatar
					src="https://source.unsplash.com/YOErFW8AfkI/128x128"
					rounded="rounded-full"
					width="w-9"
				/>
			</div>
			{#if $isProfileMenuOpen}
				<ul
					use:clickOutside={['nav-profile-photo']}
					on:click-outside={closeProfileMenu}
					use:keydownEscape
					on:keydown-escape={closeProfileMenu}
					class="absolute right-0 w-56 p-2 mt-2 space-y-2 text-gray-600 bg-white border border-gray-100 rounded-md shadow-md dark:border-gray-700 dark:text-gray-300 dark:bg-gray-700"
					aria-label="submenu"
				>
					<li class="flex">
						<a
							class="inline-flex items-center w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
							href="/"
						>
							<i class="fa-solid fa-user mr-2" />
							<span>Profile</span>
						</a>
					</li>
					<li class="flex">
						<a
							class="inline-flex items-center w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
							href="/"
						>
							<i class="fa-solid fa-gear mr-2" />
							<span>Settings</span>
						</a>
					</li>
					<li class="flex">
						<a
							class="inline-flex items-center w-full px-2 py-1 text-sm font-semibold transition-colors duration-150 rounded-md hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-800 dark:hover:text-gray-200"
							href={import.meta.env.VITE_LOGOUT_PATH}
						>
							<i class="fa-solid fa-inbox mr-2" />
							<span>Log out</span>
						</a>
					</li>
				</ul>
			{/if}
		</div>
	</svelte:fragment>
</AppBar>
