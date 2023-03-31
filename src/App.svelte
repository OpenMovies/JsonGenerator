<script lang="ts">
    import Icon from "@iconify/svelte";

    class Movie {
        title: String
        shortname: String
        description: String
        genre: Array<String> = []
        rating: String
        language: String
        cast: Array<{
            name: String
            role: String
        }>
        crew: {
            director: Array<String>
            producer: Array<String>
            writer: Array<String>
        }
        distributor: Array<String>
        boxOffice: {
            budget: String
            gross: {
                us: String
                worldwide: String
            }
            openingWeekend: {
                us: String
                worldwide: String
            }
        }
        release: {
            year: Number
            month: Number
            day: Number
        }
        countryOfOrigin: Array<String>
        runtime: {
            hours: Number
            minutes: Number
            seconds: Number
        }
    }

    let movie: Movie = new Movie();

    let _genre: String;
    function addGenre() {
        if (_genre == undefined) return;

        movie.genre.push(_genre);
        _genre = undefined;
        movie.genre = movie.genre;
    }

    function removeGenre() {
        movie.genre.pop();
        movie.genre = movie.genre;
    }

    class castMember {
        name: String
        role: String
    }

    let _castMember: castMember = new castMember();

    let cast: Array<castMember> = [];

    function addCastMember() {
        if (_castMember == undefined) return;

        cast.push(_castMember);
        _castMember = new castMember();
        cast = cast;
    }

    function removeCastMember(index: any) {
        cast.splice(index, 1)
        cast = cast;
        return index;
    }

    $: movieJson = JSON.stringify(movie);
</script>

<p class="text-center font-serif font-bold text-neutral-800 text-4xl pt-6">OpenMovies Json Generator</p>

<div class="bg-white rounded-xl justify-center mx-6 mt-6">
    <div class="flex flex-col w-full lg:flex-row">
        <div class="grid card rounded-box">
            <div class="p-2">
                <input type="text" placeholder="Title" class="input w-full my-1 rounded-xl" bind:value={movie.title} />
                <input type="text" placeholder="Shortname" class="input w-full my-1 rounded-xl" bind:value={movie.shortname} />
                <textarea class="textarea w-full my-1 rounded-xl" placeholder="Description" rows="2" bind:value={movie.description}></textarea>
                <div class="flex flex-row">
                    <p class="ml-4">Genre(s)</p>
                    {#each movie.genre as g}
                        <p class="ml-4">{g}</p>
                    {:else}
                        <p class="ml-4">No genres added</p>
                    {/each}
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addGenre}>Add</button>
                    <button class="btn btn-ghost btn-sm mr-4" on:click={removeGenre}>Remove</button>
                </div>
                <input type="text" placeholder="Add Genre" class="input w-full my-1 rounded-xl" bind:value={_genre} />
                <input type="text" placeholder="Rating" class="input w-full my-1 rounded-xl" bind:value={movie.rating} />
                <input type="text" placeholder="Language" class="input w-full my-1 rounded-xl" bind:value={movie.language} />
                <div class="flex flex-col">
                    <p class="ml-4">Cast</p>
                    {#each cast as c}
                        <div class="flex-row">
                            <p class="ml-4">{c.name} as {c.role}</p>
                            <button class="btn btn-ghost btn-sm mr-4" on:click={() => removeCastMember(c)}>Remove</button>
                        </div>
                    {:else}
                        <p class="ml-4">No cast members added</p>
                    {/each}
                </div>
                <div class="flex flex-row">
                    <input type="text" placeholder="Name" class="input my-1 rounded-xl" bind:value={_castMember.name} />
                    <input type="text" placeholder="Role" class="input my-1 rounded-xl" bind:value={_castMember.role} />
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addCastMember}>Add</button>
                </div>
            </div>
        </div>
        <div class="divider lg:divider-horizontal"><Icon icon="ph:arrows-left-right-bold" width="64" height="64" /></div>
        <div class="grid flex-grow h-32 card rounded-box">
            {movieJson}
        </div>
    </div>
</div>