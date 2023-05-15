<script lang="ts">
	import { AppBar, AppShell } from '@skeletonlabs/skeleton';
	import Sidebar from '$components/Sidebar/page.svelte';
	import HtmlHead from '$src/routes/html_head.svelte';
	import { isDark, isSideMenuOpen, closeSideMenu } from '$stores/menus';
	import { keydownEscape } from '$lib/ioevents/keydown';
	import { clickOutside } from '$lib/ioevents/click';

	// Your selected Skeleton theme:
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';

	// This contains the bulk of Skeletons required styles:
	// NOTE: this will be renamed skeleton.css in the v2.x release.
	import '@skeletonlabs/skeleton/styles/skeleton.css';

	// Finally, your application's global stylesheet (sometimes labeled 'app.css')
	import '../app.postcss';

	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';

	function scrollHandler(event: UIEvent & { currentTarget: EventTarget & HTMLDivElement }) {
		console.log(event.currentTarget.scrollTop);
	}
</script>

<HtmlHead {isDark} />

<AppShell regionPage="relative" slotPageHeader="sticky top-0 z-10" on:scroll={scrollHandler}>
	<svelte:fragment slot="pageHeader">
		<AppBar>Skeleton</AppBar>
	</svelte:fragment>
	<svelte:fragment slot="sidebarLeft">
		<div
			id="sidebar-left"
			class="hidden lg:block"
			use:clickOutside={['nav-mobile-hamburger']}
			on:click-outside={closeSideMenu}
			use:keydownEscape
			on:keydown-escape={closeSideMenu}
		>
			<Sidebar />
		</div>
	</svelte:fragment>

	<slot />
	<svelte:fragment slot="pageFooter">Page Footer</svelte:fragment>
</AppShell>
