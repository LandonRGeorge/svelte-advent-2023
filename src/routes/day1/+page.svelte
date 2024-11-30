<script>
    import { onMount } from "svelte";

    let name = $state("");
    let tally = $state("");
    let kids = $state([]);

    onMount(async () => {
        kids = [...(await getKids())];
    });

    const getKids = async () => {
        const res = await fetch(
            "https://advent.sveltesociety.dev/data/2023/day-one.json",
        );
        const data = await res.json();
        console.log(data);
        return data;
    };
</script>

<h1>Day 1 - Naughty or Nice</h1>
<form>
    <div>
        <label for="name">Name</label>
        <input type="text" id="name" name="name" bind:value={name} />
    </div>
    <div>
        <label for="tally">Tally</label>
        <input type="number" id="tally" name="tally" bind:value={tally} />
    </div>
    <button
        type="submit"
        onclick={() => {
            let newKid = {
                name,
                tally,
            };
            kids = [newKid, ...kids];
            name = "";
            tally = "";
        }}>submit</button
    >
</form>

<table>
    <thead>
        <tr>
            <th>name</th>
            <th>tally</th>
        </tr>
    </thead>
    <tbody>
        {#each kids as kid}
            <tr>
                <td>{kid.name}</td>
                <td>{kid.tally}</td>
            </tr>
        {/each}
    </tbody>
</table>

<style>
    table,
    th,
    tr,
    td {
        border: 1px solid black;
    }
    table {
        border-collapse: collapse;
    }
    th,
    td {
        padding: 0.2rem 1rem;
    }
    th {
        background-color: gray;
        color: white;
    }
</style>
