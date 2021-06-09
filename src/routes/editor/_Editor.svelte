<script lang="ts">
    import { onMount, createEventDispatcher } from 'svelte'

    type EditorData = {
        title: string,
        content: string
    }

    let editor
    let holder
    let title
    export let data: EditorData
    let dispatch = createEventDispatcher()
    let onSave = () => {
            editor.save().then((draft) => dispatch("save", draft));
    };

    onMount(async() => {
        const EditorJS = await import('@editorjs/editorjs')
        data: data.content,
        editor = new EditorJS.default({
            holder,
            placeholder: "let's pour it...",
            hideToolbar: false,
            onReady: () => {
                console.log(`Over to you dear author!`);
            },
        });
    })
</script>
<div class="editor shadow-inner border-gray-00 border-2 py-8">
    <textarea id="editorjs-heading" class="w-full mb-2 bg-gray-100 py-3 px-24 outline-none text-left text-3xl" name="heading" bind:value={title} placeholder="What are you upto today?"  />
    <div id="editorjs" bind:this={holder} class="w-full bg-gray-100 py-8 text-left text-xl" />
</div>

<button on:click={onSave}>Save</button>
