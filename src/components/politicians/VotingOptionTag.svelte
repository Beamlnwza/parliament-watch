<script lang="ts">
	import { DefaultVoteOption, type CustomVoteOption } from '$models/voting';
	import { Tag } from 'carbon-components-svelte';
	import type { TagProps } from 'carbon-components-svelte/types/Tag/Tag.svelte';

	export let voteOption: DefaultVoteOption | CustomVoteOption;

	let className = '';
	export { className as class };

	let tagColorClass = 'bg-purple-70';
	let tagBgOpacity = 1;
	let label = '';

	if (typeof voteOption === 'string') {
		switch (voteOption as DefaultVoteOption) {
			case DefaultVoteOption.Agreed:
				label = DefaultVoteOption.Agreed;
				tagColorClass = 'bg-teal-50';
				break;
			case DefaultVoteOption.Disagreed:
				label = DefaultVoteOption.Disagreed;
				tagColorClass = 'bg-red-50 text-white';
				break;
			case DefaultVoteOption.Novote:
				label = DefaultVoteOption.Novote;
				tagColorClass = 'bg-gray-80 text-white';
				break;
			case DefaultVoteOption.Abstain:
				label = DefaultVoteOption.Abstain;
				tagColorClass = 'bg-gray-50 text-white';
				break;
			case DefaultVoteOption.Absent:
				label = DefaultVoteOption.Absent;
				tagColorClass = 'bg-gray-20';
				break;
		}
	} else {
		tagColorClass = 'bg-purple-70';
		tagBgOpacity = voteOption?.colorIntensity * 0.7 + 0.3 ?? 1;
		if (tagBgOpacity > 0.45) tagColorClass += ' text-white';
		label = voteOption?.label ?? '';
	}
</script>

<Tag
	class="m-0 whitespace-nowrap {tagColorClass} {className}"
	style="--tw-bg-opacity:{tagBgOpacity}">{label}</Tag
>
