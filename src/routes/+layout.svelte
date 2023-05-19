<script lang="ts">
	import { AppBar, AppShell, storeHighlightJs } from '@skeletonlabs/skeleton';
	import Sidebar from '$components/Sidebar/page.svelte';
	import Header from '$components/Header/page.svelte';
	import { closeSideMenu } from '$stores/menus';
	import { keydownEscape } from '$lib/ioevents/keydown';
	import { clickOutside } from '$lib/ioevents/click';
	import { computePosition, autoUpdate, offset, shift, flip, arrow } from '@floating-ui/dom';
	import hljs from 'highlight.js';

	// Your selected Skeleton theme:
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';

	// This contains the bulk of Skeletons required styles:
	// NOTE: this will be renamed skeleton.css in the v2.x release.
	import '@skeletonlabs/skeleton/styles/skeleton.css';

	// Finally, your application's global stylesheet (sometimes labeled 'app.css')
	import '../app.postcss';

	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';

	import 'highlight.js/styles/github-dark.css';

	storeHighlightJs.set(hljs);
</script>

<AppShell regionPage="relative" slotPageHeader="sticky top-0 z-10" class="overflow-hidden">
	<svelte:fragment slot="pageHeader">
		<Header />
	</svelte:fragment>
	<svelte:fragment slot="sidebarLeft">
		<div
			id="sidebar-left"
			class="hidden lg:block"
			use:clickOutside={['nav-mobile-hamburger']}
			use:keydownEscape
		>
			<Sidebar />
		</div>
	</svelte:fragment>

	<slot />
	<!-- <svelte:fragment slot="pageFooter">Page Footer</svelte:fragment> -->
</AppShell>
