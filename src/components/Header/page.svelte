<script lang="ts">
	import { toggleProfileMenu, closeProfileMenu, isProfileMenuOpen } from '$stores/menus';
	import { AppBar, Avatar, ListBox, ListBoxItem } from '@skeletonlabs/skeleton';
	import { clickOutside } from '$lib/ioevents/click';
	import { keydownEscape } from '$lib/ioevents/keydown';
</script>

<AppBar gridColumns="grid-cols-3" slotDefault="place-self-center" slotTrail="place-content-end">
	<svelte:fragment slot="lead"><i class="fa-solid fa-bars text-2xl" /></svelte:fragment>
	Title
	<svelte:fragment slot="trail">
		<i class="fa-solid fa-moon fa-xl" />
		<i class="fa-solid fa-sun fa-xl" />
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
					width="w-10"
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
