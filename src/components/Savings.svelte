<script>
    import Card from "./Card.svelte";

    export let title;
    export let powerYearBefore;
    export let powerYearAfter;
    export let priceWh;
    export let priceInvestment;

    $: powerYearSaving = powerYearBefore - powerYearAfter;
    $: euroYearSaving = powerYearSaving * priceWh;
    $: paybackPeriodDays = (priceInvestment / euroYearSaving) * 365;

    $: lineColor =
        euroYearSaving > 0 ? "decoration-green-500" : "decoration-red-500";
</script>

<Card {title}>
    <div class="grid grid-cols-2 gap-4 ">
        <div>Stroom</div>
        <div class="font-bold">{powerYearSaving.toFixed(0)} kWh</div>
        <div>Bedrag</div>
        <div
            class="font-bold underline-offset-4 underline decoration-4 {lineColor}"
        >
            &euro; {euroYearSaving.toLocaleString("nl-NL", {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2,
            })}
        </div>
        <div>Terugverdiend na</div>
        <div class="font-bold">
            {#if priceInvestment == 0}
                geen investering gedaan 😐
            {:else if paybackPeriodDays == Number.POSITIVE_INFINITY || paybackPeriodDays == Number.NEGATIVE_INFINITY || paybackPeriodDays < 0}
                nooit 😔
            {:else if paybackPeriodDays > 600}
                {paybackPeriodDays.toFixed(0)} dagen 😨
            {:else}
                {paybackPeriodDays.toFixed(0)} dagen 👍
            {/if}
        </div>
    </div>
</Card>
