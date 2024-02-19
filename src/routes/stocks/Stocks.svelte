<script>
  import Chart from 'chart.js/auto';
  import colorLib from '@kurkle/color';
  import Button from '../../lib/components/page/Button.svelte';

  let ticker = '';
  let symbol = '';
  let resultSectionClass = 'hidden';
  let entries = [{ high: 0 }];

  async function stockFetch() {
    try {
      const res = await fetch(`https://financialmodelingprep.com/api/v3/historical-price-full/${ticker}?apikey=gzk82CgOGl1CIUHAXNBVlx8l3nRZGFWv`);

      if (!res.ok) {
        throw new Error(`HTTP error! status: ${res.status}`);
      }

      const jsonResult = await res.json();
      symbol = jsonResult.symbol;
      entries = jsonResult.historical;
      buildChart();
      resultSectionClass = '';
    } catch (e) {
      console.log(e);
    }
  }

  function transparentize(value, opacity) {
    var alpha = opacity === undefined ? 0.5 : 1 - opacity;
    return colorLib(value).alpha(alpha).rgbString();
  }

  function buildChart() {
    const ctx = document.getElementById('chart');

    if (!ctx || !(ctx instanceof HTMLCanvasElement)) {
      console.error('Cannot find canvas element');
      return;
    }

    // Reverse the entries array and take the last 7 entries
    const lastEntries = entries.slice(-7).reverse();

    // Generate the labels and data arrays
    const labels = lastEntries.map((entry) => entry.label.split(',')[0]);
    const data = lastEntries.map((entry) => entry.close);

    new Chart(ctx, {
      type: 'line',
      data: {
        labels,
        datasets: [
          {
            label: 'End of day stock price in $USD',
            data,
            borderColor: 'rgb(54, 162, 235)',
            backgroundColor: transparentize('rgb(54, 162, 235)', 0.5),
          },
        ],
      },
      options: {
        responsive: true,
        plugins: {
          legend: {
            position: 'top',
          },
          title: {
            display: true,
            text: 'Stock prices for provided ticker the last week',
          },
        },
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      },
    });
  }
</script>

<h1>Stock prices</h1>

<p>Enter the company stock ticker you want to search stock prices for</p>

<section>
  <form method="POST" on:submit|preventDefault={stockFetch}>
    <input bind:value={ticker} id="search" name="search" type="text" placeholder="Enter company stock ticker, e.g. tsla, eqnr or aapl" />

    <Button type="submit" buttonText="Search"></Button>
  </form>
</section>

<section class={resultSectionClass}>
  <h2>{symbol} - ${entries[0].close} ({entries[0].label})</h2>
</section>

<section>
  <canvas id="chart" width="400" height="400"></canvas>
</section>

<style>
</style>
