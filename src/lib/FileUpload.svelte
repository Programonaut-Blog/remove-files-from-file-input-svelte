<script lang="ts">
    let files: FileList;

    function removeFile(fileToRemove: File) {
        const dt = new DataTransfer();
        if (files) {
            for (let i = 0; i < files.length; i++) {
                const file = files[i];

                if (file.name !== fileToRemove.name) dt.items.add(file);
            }
        }
        files = dt.files;
    }

    $: console.log(files);
</script>

<input type="file" multiple bind:files />

{#if files}
    {#each Array.from(files) as file}
        <div>
            <button class="contrast outline" on:click={() => removeFile(file)}>❌</button>
            {file.name}
        </div>
    {/each}
{/if}

<style>
    button {
        width: max-content;
        display: inline-block;
    }
</style>
