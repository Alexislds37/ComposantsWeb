<script>
    import { onMount } from 'svelte';
    import PouchDB from 'pouchdb-browser';
    
    export let documents = [];
    export let initsrc;
    export let collection;
    let db;

    $: if (db) { load_documents(); }

    async function load_documents() {
        if (!db) return;
        const r = await db.info();
        if (r.update_seq === 0) {
            const res = await fetch(initsrc);
            documents = await res.json();
            db.bulkDocs(docs);
        }
        const zdocs = await db.allDocs({include_docs: true});
        documents = zdocs.rows.map( d=> d.doc);
    }

    onMount(async() => {
        const pdb = new PouchDB(collection);
        await pdb.info();
        db = pdb;
    });
</script>