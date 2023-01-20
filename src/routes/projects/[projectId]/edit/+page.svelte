<script>
	import { enhance } from '$app/forms';
	import { Input } from '$lib/components';
	import { Icon, Trash } from 'svelte-hero-icons';
	import { getImageURL } from '$lib/utils';

	export let data;
</script>

<div class="flex flex-col w-full h-full p-2">
	<div class="w-full">
		<form
			action="?/updateProject"
			method="POST"
			class="flex flex-col space-y-2 w-full items-center"
			enctype="multipart/form-data"
			use:enhance
		>
			<h3 class="text-3xl font-bold">
				Edit {data.project.name}
			</h3>
			<Input id="name" label="Project name" value={data.project.name ?? ''} />
			<Input id="tagline" label="Project tagline" value={data.project.tagline ?? ''} />
			<Input id="url" label="Project URL" value={data.project.url ?? ''} />
			<div class="form-control w-full max-w-lg">
				<label for="" class="label font-medium pb-1">
					<span class="label-text" />
				</label>
				<textarea
					name="description"
					class="textarea textarea-bordered h-24 resize-none"
					value={data.project.description ?? ''}
				/>
			</div>
			<div class="form-control w-full max-w-lg">
				<label for="thumbnail" class="label font-medium pb-1">
					<span class="label-text">Thumbnail</span>
				</label>
				{#if data.project.thumbnail}
					<label for="thumbnail" class="avatar w-20" hover:cursor-pointer>
						<label for="thumbnail" class="absolute -top-1 5 -right-1 5" hover:cursor-pointer>
							<button
								formaction="?/deleteThumbnail"
								type="submit"
								class="btn btn-error btn-sm btn-circle"
							>
								<Icon src={Trash} class="w-5 h-5 text-white" />
							</button>
						</label>
						<div class="w-20 rounded">
							<img
								src={data.project.thumbnail
									? getImageURL(
											data.project.collectionId,
											data.project.id,
											data.project.thumbnail,
											'80x80'
									  )
									: `https://via.placeholder.com/80/4506CB/FFFFFF/?text=${data.project.name}`}
								alt="project thumbnail"
							/>
						</div>
					</label>
				{/if}
				<input
					type="file"
					name="thumbnail"
					id="thumbnail"
					class="file-input file-input-bordered w-full max-w-lg mt-2"
				/>
			</div>
			<div class="w-full max-w-lg pt-3">
				<button class="btn btn-primary w-full max-w-lg" type="submit">Save Changes</button>
			</div>
		</form>
	</div>
</div>
