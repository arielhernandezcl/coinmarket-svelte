<script>
    let titulos = [
        "#",
        "Coin",
        "Price",
        "Price Change 24H",
        "Market Cap Change 24H",

    ];
    let monedas = [];
    const TraerMonedas = async () => {
    const respuesta = await fetch("https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false&locale=en")
    const data = await respuesta.json()
    monedas = data
    console.log(monedas)

    }

    TraerMonedas()

</script> 
<div class="container">
    <div class="row">
        <h1>CoinMarket </h1>
        <table class="table">
    <thead>
        <tr>
            {#each titulos as tabla}
            <th>{tabla}</th>
            {/each}
        </tr>
    </thead>
    <tbody>
        {#each monedas as moneda, i}
            <tr>
                <td class="text-muted">{i+1}</td>
                <td>
                <img src={moneda.image} alt={moneda.name} style="width: 3rem;" class="img-fluid me-2">
                <span>
                    {moneda.name}
                </span>
                
                <span class="text-muted text-uppercase ms-2">
                    {moneda.symbol}
                </span>
                </td>
                <td>
                   $ {moneda.current_price.toLocaleString()}
                </td>
                <td class={moneda.price_change_percentage_24h > 0 ? "text-success" : "text-danger"}>
                    {moneda.price_change_percentage_24h.toLocaleString()} %
                </td>
                <td>
                    {moneda.market_cap_change_24h}
                </td>
            
            </tr>

        {/each}       
    </tbody>
</table>
    </div>
</div>
<style>
    :global(.prose body) {
        background-color: #141414;
    }
</style>

<p>Visit <a href="https://www.arielhernandez.net">arielhernandez.net</a></p>
