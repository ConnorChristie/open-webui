<script lang="ts">
	import { getContext, createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	const i18n = getContext('i18n');

	import Tooltip from '$lib/components/common/Tooltip.svelte';
	import ArenaModelModal from './ArenaModelModal.svelte';
	import Pencil from '$lib/components/icons/Pencil.svelte';
	export let model;

	let showModel = false;
</script>

<ArenaModelModal
	bind:show={showModel}
	edit={true}
	{model}
	on:submit={async (e) => {
		dispatch('edit', e.detail);
	}}
	on:delete={async () => {
		dispatch('delete');
	}}
/>

<div class="py-0.5">
	<div class="flex justify-between items-center mb-1">
		<div class="flex flex-col flex-1">
			<div class="flex gap-2.5 items-center">
				<img
					src={model.meta.profile_image_url}
					alt={model.name}
					class="size-8 rounded-full object-cover shrink-0"
				/>

				<div class="w-full flex flex-col">
					<div class="flex items-center gap-1">
						<div class="shrink-0 line-clamp-1">
							{model.name}
						</div>
					</div>

					<div class="flex items-center gap-1">
						<div class=" text-xs w-full text-gray-500 bg-transparent line-clamp-1">
							{model?.meta?.description ?? model.id}
						</div>
					</div>
				</div>
			</div>
		</div>

		<div class="flex items-center">
			<Tooltip content={$i18n.t('Edit Arena Model')}>
				<button
					class="self-center w-fit text-sm p-1.5 dark:text-gray-300 dark:hover:text-white hover:bg-black/5 dark:hover:bg-white/5 rounded-xl"
					type="button"
					on:click={() => {
						showModel = true;
					}}
				>
					<Pencil />
				</button>
			</Tooltip>
		</div>
	</div>
</div>
