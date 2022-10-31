<script>
    import PricePerDayCalculator from "../components/PricePerDayCalculator.svelte";
    import Input from "../components/Input.svelte";
    import Card from "./Card.svelte";
    import Savings from "../components/Savings.svelte";

    let priceWh = 0.4;
    let priceInvestment = 100;
    let powerYearBefore = "";
    let powerYearAfter = "";
</script>

<div class="grid grid-cols-4 gap-4">
    <div class="col-span-4 md:col-span-2 lg:col-span-1">
        <Card title="Kosten 💸">
            <Input
                label="Stroomprijs in euro per kWh"
                step="0.01"
                maxlength="6"
                bind:value={priceWh}
            />
            <Input label="Investering in euro" bind:value={priceInvestment} />
        </Card>
    </div>
    <div class="col-span-4 md:col-span-2 lg:col-span-1">
        <Savings
            title="Besparing per jaar 💰"
            {powerYearBefore}
            {powerYearAfter}
            {priceWh}
            {priceInvestment}
        />
    </div>
    <div class="col-span-4 md:col-span-2">
        <Card title="Wat is dit? 🤔">
            Als je stroomkosten wilt besparen, is het handig als je het eerst
            even doorrekent. Met deze tool kun je berekenen hoe lang het duurt
            voordat je je investering hebt terugverdiend. Als je niets
            investeert, kun je uitrekenen hoeveel je per jaar bespaart als je
            minder stroom gaat gebruiken.
        </Card>
    </div>

    <div class="col-span-4 md:col-start-1 md:col-span-2">
        <PricePerDayCalculator
            title="Situatie voor de investering 🧓🏻"
            {priceWh}
            powerOne={100}
            bind:totalkWh={powerYearBefore}
        />
    </div>
    <div class="col-span-4 md:col-span-2">
        <PricePerDayCalculator
            title="Situatie na de investering 👼"
            {priceWh}
            bind:totalkWh={powerYearAfter}
        />
    </div>
</div>
