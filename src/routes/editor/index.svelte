<script context="module">
	export const ssr = false;
</script>
<script>
	import Editor from './_Editor.svelte'
	let post = { title: '', content: '' }
    let onSave = (draft) => {
        console.log('from parent', draft.detail)
    };
</script>

<Editor data={post} on:save={onSave} />
