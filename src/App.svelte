<script lang="ts">
    import Icon from "@iconify/svelte";

    let title: String;
    let shortname: String;
    let description: String;

    let _genre: String;
    let genres: Array<String> = [];
    function addGenre() {
        if (_genre == undefined) return;

        genres.push(_genre);
        _genre = undefined;
        genres = genres;
    }

    function removeGenre() {
        genres.pop();
        genres = genres;
    }

    let rating: String;
    let language: String;
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
                    {#each genres as g}
                        <p class="ml-4">{g}</p>
                    {:else}
                        <p class="ml-4">No genres added</p>
                    {/each}
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addGenre}>Add</button>
                    <button class="btn btn-ghost btn-sm mr-4" on:click={removeGenre}>Remove</button>
                </div>
                <input type="text" placeholder="Add Genre" class="input w-full my-1 rounded-xl" bind:value={_genre} />
                <input type="text" placeholder="Rating" class="input w-full my-1 rounded-xl" bind:value={rating} />
                <input type="text" placeholder="Language" class="input w-full my-1 rounded-xl" bind:value={language} />
            </div>
        </div>
        <div class="divider lg:divider-horizontal"><Icon icon="ph:arrows-left-right-bold" width="64" height="64" /></div>
        <div class="grid flex-grow h-32 card rounded-box"></div>
    </div>
</div>