<script>
  import { Router, Route } from 'svelte-routing';

  import Layout from './lib/components/layout/_layout.svelte';
  import Home from './routes/home/Home.svelte';
  import Cats from './routes/cats/Cats.svelte';
  import Stocks from './routes/stocks/Stocks.svelte';
</script>

<Router>
  <Layout>
    <Route path="/" component={Home}></Route>
    <Route path="/cats" component={Cats}></Route>
    <Route path="/stocks" component={Stocks}></Route>
</Layout>
</Router>

<style>
  /* Add any necessary styles here */
</style>
