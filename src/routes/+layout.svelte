<script>
    let { children } = $props();
</script>

<nav>
    <h2>
        <a href="/">Advent of Svelte 2023</a>
    </h2>
    <a href="https://advent.sveltesociety.dev/#challenges" target="_blank"
        >Challenge Site</a
    >
</nav>
<main>
    {@render children()}
</main>

<style>
    :global(html) {
        box-sizing: border-box;
    }
    :global(*),
    :global(*::before),
    :global(*::after) {
        margin: 0;
        padding: 0;
        box-sizing: inherit;
    }
    :global(a) {
        text-decoration: none;
        color: unset;
    }
    :global(a:hover) {
        text-decoration: underline;
    }
    nav {
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: blue;
        padding: 1rem 2rem;
        color: white;
    }
    main {
        margin: 0 2rem;
        margin-top: 1rem;
    }
</style>
