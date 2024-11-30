<script>
    import { onMount } from "svelte";
    let heartRate = $state("waiting...");
    onMount(async () => {
        setInterval(async () => {
            heartRate = await getHeartRate();
        }, 1000);
    });
    async function getHeartRate() {
        let res = await fetch(
            "https://advent.sveltesociety.dev/data/2023/day-four.json",
        );
        let { heartRate } = await res.json();
        return heartRate;
    }
</script>

<div>Heart Rate: {heartRate}</div>
