<script lang="ts">
	import { CodeBlock } from '@skeletonlabs/skeleton';

	import DocsPreview from '$docs/components/DocsPreview/page.svelte';
</script>

<svelte:head>
	<title>Codes</title>
</svelte:head>

<main class="h-full pb-16 overflow-y-auto">
	<div class="container grid px-6 mx-auto">
		<h2 class="my-6 text-2xl font-semibold text-gray-700 dark:text-gray-200">Modals</h2>

		<div class="mt-4">
			<DocsPreview>
				<svelte:fragment slot="preview">
					<div class="w-full space-y-4">
						<CodeBlock language="html" code={`<div>This is meta</div>`} />
						<CodeBlock language="css" code={`.skeleton { color: #bada55; }`} />
						<CodeBlock language="ts" code={`const skeleton: string = 'awesome';`} />
					</div>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock
						language="html"
						code={`<CodeBlock language="html" code={\`<div>This is meta</div>\`}></CodeBlock>`}
					/>
					<CodeBlock
						language="html"
						code={`<CodeBlock language="css" code={\`.skeleton { color: #bada55; }\`}></CodeBlock>`}
					/>
					<CodeBlock
						language="html"
						code={`<CodeBlock language="ts" code={\`const skeleton: string = 'awesome';\`}></CodeBlock>`}
					/>
				</svelte:fragment>
			</DocsPreview>
		</div>
	</div>
</main>
