<script>
    const fetchData = (async () => {
        const res = await fetch('http://localhost:8888/tailwind/wp-json/wp/v2/posts')
        return await res.json()
    })()

</script>

{#await fetchData}
<p>...getting posts</p>

{:then data}
    {#each data as post, i}
        <div class="post">{post.title.rendered}</div>
    {/each}
{:catch error}
    <p>No posts found.</p>
{/await}