<script>
    let tally = $state(0);
</script>

<h1>Day 2 - Merry Munch-o-Meter</h1>
<div>
    <button onclick={() => tally++}>Increment</button>
    <button onclick={() => tally--}>Decrement</button>
    <button onclick={() => (tally = 0)}>Reset</button>
</div>
<div>{tally} {tally === 1 ? "Cookie" : "Cookies"}</div>
