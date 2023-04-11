<script lang="ts">
    import Icon from "@iconify/svelte";

    class Movie {
        title: String = ""
        shortname: String = ""
        description: String = ""
        genre: Array<String> = []
        rating: String = ""
        language: String = ""
        cast: Array<{
            name: String
            role: String
        }> = []
        crew: {
            director: Array<String>
            producer: Array<String>
            writer: Array<String>
        } = {
            director: [],
            producer: [],
            writer: []
        }
        distributor: Array<String> = []
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
        } = {
            budget: "",
            gross: {
                us: "",
                worldwide: ""
            },
            openingWeekend: {
                us: "",
                worldwide: ""
            }
        }
        release: {
            year: Number
            month: Number
            day: Number
        } = {
            year: 0,
            month: 0,
            day: 0
        }
        countryOfOrigin: Array<String> = []
        runtime: {
            hours: Number
            minutes: Number
            seconds: Number
        } = {
            hours: 0,
            minutes: 0,
            seconds: 0
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

    function addCastMember() {
        if (_castMember == undefined) return;

        movie.cast.push(_castMember);
        _castMember = new castMember();
        movie.cast = movie.cast;
    }

    function removeCastMember(index: any) {
        movie.cast.splice(index, 1)
        movie.cast = movie.cast;
        return index;
    }

    let _director: String;

    function addDirector() {
        if (_director == undefined) return;

        movie.crew.director.push(_director);
        _director = undefined;
        movie.crew.director = movie.crew.director;
    }

    function removeDirector(index: any) {
        movie.crew.director.splice(index, 1)
        movie.crew.director = movie.crew.director;
        return index;
    }

    let _producer: String;

    function addProducer() {
        if (_producer == undefined) return;

        movie.crew.producer.push(_producer);
        _producer = undefined;
        movie.crew.producer = movie.crew.producer;
    }

    function removeProducer(index: any) {
        movie.crew.producer.splice(index, 1)
        movie.crew.producer = movie.crew.producer;
        return index;
    }

    let _writer: String;

    function addWriter() {
        if (_writer == undefined) return;

        movie.crew.writer.push(_writer);
        _writer = undefined;
        movie.crew.writer = movie.crew.writer;
    }

    function removeWriter(index: any) {
        movie.crew.writer.splice(index, 1)
        movie.crew.writer = movie.crew.writer;
        return index;
    }

    let _distributor: String;

    function addDistributor() {
        if (_distributor == undefined) return;

        movie.distributor.push(_distributor);
        _distributor = undefined;
        movie.distributor = movie.distributor;
    }

    function removeDistributor(index: any) {
        movie.distributor.splice(index, 1)
        movie.distributor = movie.distributor;
        return index;
    }

    $: movieJson = JSON.stringify(movie, null, 2);
</script>

<p class="text-center font-serif font-bold text-neutral-800 text-4xl pt-6">OpenMovies Json Generator</p>

<div class="bg-white rounded-xl justify-center mx-6 mt-6">
    <div class="flex flex-col w-full lg:flex-row">
        <div class="grid card rounded-box">
            <div class="p-2">
                <input type="text" placeholder="Title" class="input w-full my-1 rounded-xl" bind:value={movie.title}/>
                <input type="text" placeholder="Shortname" class="input w-full my-1 rounded-xl"
                       bind:value={movie.shortname}/>
                <textarea class="textarea w-full my-1 rounded-xl" placeholder="Description" rows="2"
                          bind:value={movie.description}></textarea>
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
                <input type="text" placeholder="Add Genre" class="input w-full my-1 rounded-xl" bind:value={_genre}/>
                <input type="text" placeholder="Rating" class="input w-full my-1 rounded-xl" bind:value={movie.rating}/>
                <input type="text" placeholder="Language" class="input w-full my-1 rounded-xl"
                       bind:value={movie.language}/>
                <div class="flex flex-col">
                    <p class="ml-4">Cast</p>
                    {#each movie.cast as c}
                        <div class="flex-row">
                            <p class="ml-4">{c.name} as {c.role}</p>
                            <button class="btn btn-ghost btn-sm mr-4" on:click={() => removeCastMember(c)}>Remove
                            </button>
                        </div>
                    {:else}
                        <p class="ml-4">No cast members added</p>
                    {/each}
                </div>
                <div class="flex flex-row">
                    <input type="text" placeholder="Name" class="input my-1 rounded-xl" bind:value={_castMember.name}/>
                    <input type="text" placeholder="Role" class="input my-1 rounded-xl" bind:value={_castMember.role}/>
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addCastMember}>Add</button>
                </div>
                <div class="flex flex-col">
                    <p class="ml-4">Director</p>
                    {#each movie.crew.director as d}
                        <div class="flex-row">
                            <p class="ml-4">{d}</p>
                            <button class="btn btn-ghost btn-sm mr-4" on:click={() => removeDirector(d)}>Remove</button>
                        </div>
                    {:else}
                        <p class="ml-4">No directors added</p>
                    {/each}
                </div>
                <div class="flex flex-row">
                    <input type="text" placeholder="Name" class="input my-1 rounded-xl" bind:value={_director}/>
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addDirector}>Add</button>
                </div>
                <div class="flex flex-col">
                    <p class="ml-4">Producer</p>
                    {#each movie.crew.producer as p}
                        <div class="flex-row">
                            <p class="ml-4">{p}</p>
                            <button class="btn btn-ghost btn-sm mr-4" on:click={() => removeProducer(p)}>Remove</button>
                        </div>
                    {:else}
                        <p class="ml-4">No producers added</p>
                    {/each}
                </div>
                <div class="flex flex-row">
                    <input type="text" placeholder="Name" class="input my-1 rounded-xl" bind:value={_producer}/>
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addProducer}>Add</button>
                </div>
                <div class="flex flex-col">
                    <p class="ml-4">Writer</p>
                    {#each movie.crew.writer as w}
                        <div class="flex-row">
                            <p class="ml-4">{w}</p>
                            <button class="btn btn-ghost btn-sm mr-4" on:click={() => removeWriter(w)}>Remove</button>
                        </div>
                    {:else}
                        <p class="ml-4">No writers added</p>
                    {/each}
                </div>
                <div class="flex flex-row">
                    <input type="text" placeholder="Name" class="input my-1 rounded-xl" bind:value={_writer}/>
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addWriter}>Add</button>
                </div>
                <div class="flex flex-col">
                    <p class="ml-4">Distributor</p>
                    {#each movie.distributor as d}
                        <div class="flex-row">
                            <p class="ml-4">{d}</p>
                            <button class="btn btn-ghost btn-sm mr-4" on:click={() => removeDistributor(d)}>Remove
                            </button>
                        </div>
                    {:else}
                        <p class="ml-4">No distributors added</p>
                    {/each}
                </div>
                <div class="flex flex-row">
                    <input type="text" placeholder="Name" class="input my-1 rounded-xl" bind:value={_distributor}/>
                    <button class="btn btn-ghost btn-sm ml-auto mr-4" on:click={addDistributor}>Add</button>
                </div>
                <p class="ml-4">Box Office</p>
            </div>
        </div>
        <div class="divider lg:divider-horizontal">
            <Icon icon="ph:arrows-left-right-bold" width="64" height="64"/>
        </div>
        <div class="grid flex-grow h-32 card rounded-box">
            <pre>
                <p>{movieJson}</p>
            </pre>
        </div>
    </div>
</div>