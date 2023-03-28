<script lang="ts">
    import Icon from "@iconify/svelte";

    let title: String;
    let shortname: String;
    let description: String;

    function addGenre() {
        console.log("addGenre");
    }
</script>

<p class="text-center text-black font-serif font-bold text-neutral-800 text-4xl pt-6">OpenMovies Json Generator</p>

<div class="bg-white rounded-xl justify-center mx-6 mt-6">
    <div class="flex flex-col w-full lg:flex-row">
        <div class="grid card rounded-box">
            <div class="p-2">
                <input type="text" placeholder="Title" class="input w-full my-1 rounded-xl" bind:value={title} />
                <input type="text" placeholder="Shortname" class="input w-full my-1 rounded-xl" bind:value={shortname} />
                <textarea class="textarea w-full my-1 rounded-xl" placeholder="Description" rows="2" bind:value={description}></textarea>
                <div class="flex flex-row">
                    <p class="ml-4">Genre(s)</p>
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addGenre}>Add</button>
                    <button class="btn btn-ghost btn-sm mr-4">Remove</button>
                </div>
                <input type="text" placeholder="Genre" class="input w-full my-1 rounded-xl" />
            </div>
        </div>
        <div class="divider lg:divider-horizontal"><Icon icon="ph:arrows-left-right-bold" width="64" height="64" /></div>
        <div class="grid flex-grow h-32 card rounded-box"></div>
    </div>
</div>