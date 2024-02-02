<script>
import { Router, Route } from 'svelte-routing';

import Layout from './lib/components/layout/_layout.svelte';
import About from './routes/about/About.svelte';
import Home from './routes/home/Home.svelte';
import News from './routes/news/News.svelte';
</script>

<Router>
  <Layout>
  <Route path="/" component={Home}></Route>
  <Route path="/news" component={News}></Route>
  <Route path="/about" component={About}></Route>
</Layout>
</Router>

<style>
  /* Add any necessary styles here */
</style>
