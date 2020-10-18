<script>
    import {fly,fade} from 'svelte/transition';
    const fetchData = (async () => {
        const res = await fetch('http://localhost:8888/tailwind/wp-json/wp/v2/posts')
        return await res.json()
    })()

</script>

{#await fetchData}
<p>...getting posts</p>

{:then data}
    {#each data as post, i}
        <div transition:fly={{y:250+1*i,delay: i * 80}} class="post" id={i}>{post.title.rendered}</div>
    {/each}
{:catch error}
    <p>No posts found.</p>
{/await}