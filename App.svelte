<script>
    let books = [];
    import TinyDB from './TinyDB.svelte';
</script>

<main>
    <TinyDB bind:documents={books} initsrc="./books.json" collection="books"/>
    <h1>Tiny Amazon</h1>
    <ul>
        {#each books as b}
        <li>{b.title}</li>
        {/each}
    </ul>

</main>
