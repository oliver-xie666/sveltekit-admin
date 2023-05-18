<script lang="ts">
	const fieldSettings: {
		inputs: {
			title: string;
			type: HTMLInputElement['type'];
			placeholder?: string;
			readonly?: boolean;
			disabled?: boolean;
			multiple?: boolean;
			autocomplete?: string;
			tabindex?: string;
		}[];
	} = {
		inputs: [
			{ title: 'Input (text)', type: 'text', placeholder: 'input text' },
			{
				title: 'Input (readonly)',
				type: 'text',
				placeholder: 'input readonly',
				readonly: true,
				tabindex: '-1'
			},
			{ title: 'Input (disabled)', type: 'text', placeholder: 'input disabled', disabled: true },
			{
				title: 'Input (email)',
				type: 'email',
				placeholder: 'john@example.com',
				autocomplete: 'email'
			},
			{
				title: 'Input (email, multiple)',
				type: 'email',
				multiple: true,
				placeholder: 'john@example.com, susy@example.com'
			},
			{ title: 'Input (password)', type: 'password', placeholder: 'password' },
			{ title: 'Input (search)', type: 'search', placeholder: 'Search...' },
			{ title: 'Input (date)', type: 'date' },
			{ title: 'Input (datetime-local)', type: 'datetime-local' },
			{ title: 'Input (month)', type: 'month' },
			{ title: 'Input (number)', type: 'number' },
			{ title: 'Input (time)', type: 'time' },
			{ title: 'Input (week)', type: 'week' },
			{ title: 'Input (tel)', type: 'tel', multiple: true, placeholder: '+61 123 456 789' },
			{ title: 'Input (url)', type: 'url', multiple: true, placeholder: 'example.com' }
		]
	};
	let currentInput: any = fieldSettings.inputs[0];
	let colorValue = '#bada55';
	function mapInputAttributes(obj: any): any {
		return Object.keys(obj)
			.map((key: any) => `${key}="${obj[key]}"`)
			.join(' ');
	}
</script>

<svelte:head>
	<title>Forms</title>
</svelte:head>

<main class="h-full pb-16 overflow-y-auto">
	<div class="container px-6 mx-auto grid">
		<h2 class="my-6 text-2xl font-semibold text-gray-700 dark:text-gray-200">Forms</h2>
		<div class="card p-4 w-full text-token space-y-4">
			<label class="label">
				<span>Input</span>
				<input class="input" type="text" placeholder="Input" />
			</label>
			<label class="label">
				<span>Select</span>
				<select class="select">
					<option value="1">Option 1</option>
					<option value="2">Option 2</option>
					<option value="3">Option 3</option>
					<option value="4">Option 4</option>
					<option value="5">Option 5</option>
				</select>
			</label>
			<label class="label">
				<span>Textarea</span>
				<!-- cspell:disable-next-line -->
				<textarea
					class="textarea"
					rows="4"
					placeholder="Lorem ipsum dolor sit amet consectetur adipisicing elit."
				/>
			</label>
		</div>
		<div class="card mt-6 p-4 pt-0">
			<div class="w-full mt-4">
				<label class="label">
					<span>Label</span>
					<input class="input" type="text" placeholder="Input" />
				</label>
			</div>
			<div class="w-full space-y-4 mt-4">
				<label class="label">
					<span>{currentInput.title}</span>
					<input class="input" {...currentInput} />
				</label>
				<div class="flex justify-center">
					<select class="select w-auto" bind:value={currentInput}>
						{#each fieldSettings.inputs as fs}<option value={fs}>{fs.title}</option>{/each}
					</select>
				</div>
			</div>
			<div class="w-full space-y-4 mt-4">
				<label class="label">
					<span>Input (file)</span>
					<input class="input" type="file" />
				</label>
				<label class="label">
					<span>Input (file, multiple)</span>
					<input class="input" type="file" multiple />
				</label>
			</div>
			<div class="w-full space-y-4 mt-4">
				<label class="label">
					<span>Textarea</span>
					<textarea class="textarea" rows="4" placeholder="Enter some long form content." />
				</label>
			</div>
			<div class="w-full space-y-4 mt-4">
				<label class="label">
					<span>Select</span>
					<select class="select">
						<option value="1">Option 1</option>
						<option value="2">Option 2</option>
						<option value="3">Option 3</option>
						<option value="4">Option 4</option>
						<option value="5">Option 5</option>
					</select>
				</label>
				<label class="label">
					<span>Select (size)</span>
					<select class="select" size="4" value="1">
						<option value="1">Option 1</option>
						<option value="2">Option 2</option>
						<option value="3">Option 3</option>
						<option value="4">Option 4</option>
						<option value="5">Option 5</option>
					</select>
				</label>
				<label class="label">
					<span>Select (multiple)</span>
					<select class="select" multiple value={['1', '2']}>
						<option value="1">Option 1</option>
						<option value="2">Option 2</option>
						<option value="3">Option 3</option>
						<option value="4">Option 4</option>
						<option value="5">Option 5</option>
					</select>
				</label>
			</div>
			<div class="space-y-2 mt-4">
				<span>Checkbox</span>
				<label class="flex items-center space-x-2">
					<input class="checkbox" type="checkbox" checked />
					<p>Option 1</p>
				</label>
				<label class="flex items-center space-x-2">
					<input class="checkbox" type="checkbox" />
					<p>Option 2</p>
				</label>
				<label class="flex items-center space-x-2">
					<input class="checkbox" type="checkbox" />
					<p>Option 3</p>
				</label>
			</div>
			<div class="space-y-2 mt-4">
				<span>Radio Group</span>
				<label class="flex items-center space-x-2">
					<input class="radio" type="radio" checked name="radio-direct" value="1" />
					<p>Option 1</p>
				</label>
				<label class="flex items-center space-x-2">
					<input class="radio" type="radio" name="radio-direct" value="2" />
					<p>Option 2</p>
				</label>
				<label class="flex items-center space-x-2">
					<input class="radio" type="radio" name="radio-direct" value="3" />
					<p>Option 3</p>
				</label>
			</div>
			<div class="w-full mt-4">
				<span>Range</span>
				<input type="range" value="75" max="100" />
			</div>
			<div class="mt-4">
				<span>Color</span>
				<div class="flex mt-2">
					<input class="input" type="color" bind:value={colorValue} />
					<input class="input" type="text" bind:value={colorValue} readonly tabindex="-1" />
				</div>
			</div>
			<div class="mt-4">
				<span>Input Group</span>
				<div class="w-full grid grid-cols-2 md:grid-cols-2 gap-6 mt-4">
					<label class="label">
						<span>Website</span>
						<div class="input-group input-group-divider grid-cols-[auto_1fr_auto]">
							<div class="input-group-shim">https://</div>
							<input type="text" placeholder="www.example.com" />
						</div>
					</label>
					<!-- --- -->
					<label class="label">
						<span>Amount</span>
						<div class="input-group input-group-divider grid-cols-[auto_1fr_auto]">
							<div class="input-group-shim"><i class="fa-solid fa-dollar-sign" /></div>
							<input type="text" placeholder="Amount" />
							<select>
								<option>USD</option>
								<option>CAD</option>
								<option>EURO</option>
							</select>
						</div>
					</label>
					<!-- --- -->
					<label class="label">
						<span>Username</span>
						<div class="input-group input-group-divider grid-cols-[1fr_auto]">
							<input type="text" placeholder="Enter Username..." />
							<a href="/elements/forms" title="Username already in use.">
								<i class="fa-solid fa-circle-exclamation text-warning-500 animate-pulse" />
							</a>
						</div>
					</label>
					<!-- --- -->
					<label class="label">
						<span>Search</span>
						<div class="input-group input-group-divider grid-cols-[auto_1fr_auto]">
							<div class="input-group-shim"><i class="fa-solid fa-search" /></div>
							<input type="search" placeholder="Search..." />
							<button class="variant-filled-secondary">Submit</button>
						</div>
					</label>
				</div>
			</div>
			<div class="mt-4">
				<span>Variants</span>
				<div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
					<label class="label">
						<span>Input (text)</span>
						<input class="input variant-form-material" type="text" placeholder="input text" />
					</label>
					<label class="label">
						<span>Input (password)</span>
						<input
							class="input variant-form-material"
							type="password"
							placeholder="Enter password..."
						/>
					</label>
					<label class="label">
						<span>Select</span>
						<select class="select variant-form-material">
							<option value="1">Option 1</option>
							<option value="2">Option 2</option>
							<option value="3">Option 3</option>
							<option value="4">Option 4</option>
							<option value="5">Option 5</option>
						</select>
					</label>
				</div>
			</div>
			<div class="mt-4">
				<span>Variants Class</span>
				<div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
					<label class="space-y-3">
						<code class="code">.input-success</code>
						<input type="text" placeholder="success" class="input input-success" />
					</label>
					<label class="space-y-3">
						<code class="code">.input-warning</code>
						<input type="text" placeholder="warning" class="input input-warning" />
					</label>
					<label class="space-y-3">
						<code class="code">.input-error</code>
						<input type="text" placeholder="error" class="input input-error" />
					</label>
				</div>
			</div>
		</div>
	</div>
</main>
