<script>
    import { onMount } from "svelte";

    let presents = $state([]);
    let sortAsc = $state(true);
    let sortField = $state("");
    let newPresents = $derived(presents);
    let selected = $state([]);
    let totalWeight = $derived(
        newPresents.filter((p) => p.selected).reduce((a, b) => a + b.weight, 0),
    );

    onMount(async () => {
        presents = await getPresents();
        presents = presents.map((p) => ({ ...p, selected: false }));
    });

    async function getPresents() {
        let res = await fetch(
            "https://advent.sveltesociety.dev/data/2023/day-three.json",
        );
        let data = await res.json();
        return data;
    }

    function handleSort(field) {
        let newSortAsc = !sortAsc;
        sortAsc = newSortAsc;
        if (newSortAsc) {
            newPresents.sort((a, b) => (a[field] > b[field] ? 1 : -1));
        } else {
            newPresents.sort((a, b) => (a[field] < b[field] ? 1 : -1));
        }
    }
</script>

<h1>Jingle Bell Balancer</h1>
<div>
    Total Weight (kg): {totalWeight.toFixed(2)}
</div>
<table>
    <thead>
        <tr>
            <th onclick={() => handleSort("name")}>Name</th>
            <th onclick={() => handleSort("weight")}>Present Weight (kg)</th>
        </tr>
    </thead>
    <tbody>
        {#each newPresents as present}
            <tr
                class={present.selected && "selected"}
                onclick={() => {
                    present.selected = !present.selected;
                }}
            >
                <td>{present.name}</td>
                <td>{present.weight.toFixed(2)}</td>
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
        cursor: pointer;
    }
    tr {
        user-select: none;
        cursor: pointer;
    }
    tr.selected {
        background-color: green;
    }
</style>
