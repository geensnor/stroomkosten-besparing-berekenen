<script>
    import { onMount } from "svelte";
    import Input from "./Input.svelte";
    import Card from "./Card.svelte";

    export let priceWh;
    export let title;
    export let powerOne = 10;
    export let totalkWh;

    let hoursOne = 12;
    let hoursTwo = 12;

    let powerTwo = 3;

    $: costOne = calculateCostYear(powerOne, hoursOne, priceWh);
    $: costTwo = calculateCostYear(powerTwo, hoursTwo, priceWh);
    $: totalCost = parseFloat(costOne) + parseFloat(costTwo);

    function calculateCostYear(power, hours, priceWh) {
        return ((power * hours * priceWh) / 1000) * 365;
    }

    const calculateTotalkWh = () => {
        totalkWh = ((hoursOne * powerOne + hoursTwo * powerTwo) / 1000) * 365;
    };

    const hoursOneChange = () => {
        hoursTwo = 24 - hoursOne;
        calculateTotalkWh();
    };
    const hoursTwoChange = () => {
        hoursOne = 24 - hoursTwo;
        calculateTotalkWh();
    };

    onMount(() => {
        hoursOneChange();
        hoursTwoChange();
    });
</script>

<Card {title}>
    <div class="grid grid-cols-3 gap-y-4 ">
        <div>
            <Input
                label="uren per dag"
                maxlength="2"
                bind:value={hoursOne}
                on:input={hoursOneChange}
            />
        </div>
        <div>
            <Input
                label="watt"
                maxlength="6"
                bind:value={powerOne}
                on:input={calculateTotalkWh}
            />
        </div>
        <div class="grid items-center justify-items-end mr-7">
            &euro; {costOne.toLocaleString("nl-NL", {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2,
            })} p/j
        </div>
        <div>
            <Input
                label="uren per dag"
                maxlength="2"
                bind:value={hoursTwo}
                on:input={hoursTwoChange}
            />
        </div>
        <div>
            <Input
                label="watt"
                maxlength="6"
                bind:value={powerTwo}
                on:input={calculateTotalkWh}
            />
        </div>
        <div class="grid items-center justify-items-end mr-7">
            &euro; {costTwo.toLocaleString("nl-NL", {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2,
            })} p/j
        </div>

        <div class="grid place-items-center col-start-2 font-bold">
            {Math.round(totalkWh, 2)} kWh p/j
        </div>
        <div class="grid place-items-end font-bold mr-7">
            &euro; {totalCost.toLocaleString("nl-NL", {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2,
            })} p/j
        </div>
    </div>
</Card>
