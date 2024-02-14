<script>
    import Chart from 'chart.js/auto';
    import colorLib from '@kurkle/color';

    let ticker = "";
    let symbol = "";
    let resultSectionClass  = "hidden";
    var entries = [{high: 0}];

    async function stockFetch() {
        try {
            const res = await fetch(
                `https://financialmodelingprep.com/api/v3/historical-price-full/${ticker}?apikey=gzk82CgOGl1CIUHAXNBVlx8l3nRZGFWv`,
            );

            var jsonResult = await res.json();
            symbol = jsonResult.symbol;
            entries = jsonResult.historical;
            buildChart();
            resultSectionClass = "";
            
        } catch (e) {
            console.log(e);
        }
    }

    function transparentize(value, opacity) {
        var alpha = opacity === undefined ? 0.5 : 1 - opacity;
        return colorLib(value).alpha(alpha).rgbString();
    }

    function buildChart() {
        const ctx = document.getElementById("chart");

        new Chart(ctx, {
            type: 'line',
            data: {
                labels: [
                    entries[6].label.split(',')[0],
                    entries[5].label.split(',')[0],
                    entries[4].label.split(',')[0],
                    entries[3].label.split(',')[0],   
                    entries[2].label.split(',')[0], 
                    entries[1].label.split(',')[0], 
                    entries[0].label.split(',')[0]
                ],
                datasets: [
                    {
                        label: 'End of day stock price in $USD',
                        data: [
                            entries[6].close,
                            entries[5].close,
                            entries[4].close,
                            entries[3].close,
                            entries[2].close, 
                            entries[1].close, 
                            entries[0].close
                        ],
                        borderColor: 'rgb(54, 162, 235)',
                        backgroundColor: transparentize('rgb(54, 162, 235)', 0.5),
                    }
                ]
            },
            options: {
                responsive: true,
                plugins: {
                    legend: {
                        position: 'top'
                    },
                    title: {
                        display: true,
                        text: "Stock prices for provided ticker the last week"
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true
                    }   
                } 
            }
        });
    }
</script>

<h1>Stock prices</h1>

<p>Enter the company stock ticker you want to search stock prices for</p>

<section>
    <form method="POST" on:submit|preventDefault={stockFetch}>
      <input
        bind:value={ticker}
        id="search"
        name="search"
        type="text"
        placeholder="Enter company stock ticker, e.g. tsla, eqnr or aapl"
      />
  
      <button type="submit">Search</button>
    </form>
</section>

<!-- <section class={resultSectionClass}>
    <h2>{symbol} - ${entries[0].close} ({entries[0].label})</h2>
    {#each entries as entry}
        <p>{entry.close}</p>
    {/each}
</section> -->

<section>
    <canvas id="chart" width="400" height="400"></canvas>
</section>

<style>
</style>
