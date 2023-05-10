<script lang="ts">
	import { AppBar, AppShell } from '@skeletonlabs/skeleton';

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

<AppShell regionPage="relative" slotPageHeader="sticky top-0 z-10" on:scroll={scrollHandler}>
	<svelte:fragment slot="pageHeader">
		<AppBar>Skeleton</AppBar>
	</svelte:fragment>
	<svelte:fragment slot="sidebarLeft">
		<div id="sidebar-left" class="hidden lg:block">Sidebar</div>
	</svelte:fragment>
	<!-- (sidebarRight) -->
	<!-- (pageHeader) -->
	<!-- Router Slot -->
	<slot />
	<!-- ---- / ---- -->
	<svelte:fragment slot="pageFooter">Page Footer</svelte:fragment>
	<!-- (footer) -->
</AppShell>
