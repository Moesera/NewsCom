<script>
  import Button from "../../lib/components/page/Button.svelte";

  let country = "";
  let uniData = [];

  async function apiFetch() {
    try {
      const res = await fetch(`http://universities.hipolabs.com/search?country=${country}`);

      uniData = await res.json();
    } catch (e) {
      console.log(e);
    }
  }
</script>

<h1>University search</h1>

<p>Enter the country you want to list universities for</p>

<section>
  <form method="POST" on:submit|preventDefault={apiFetch}>
    <!-- <label for="search" >search</label> -->
    <input bind:value={country} id="search" name="search" type="text" placeholder="Enter country" />

    <Button type="submit" buttonText="submit"></Button>
  </form>
</section>

<section class="resultSection">
  {#each uniData as uni}
    <div class="uniBoxResult">
      <h3>{uni.name}</h3>
      <a href={uni.web_pages[0]}>{uni.web_pages[0]}</a>
      <span class="badge float-right">{uni.country}</span>
    </div>
  {/each}
</section>

<style>
  .resultSection {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-top: 30px;
  }

  .uniBoxResult {
    padding: 0.8rem;
    border-radius: 6px;
    border: 1px solid #ddd;
  }

  .uniBoxResult h3 {
    margin-top: 5px;
  }
</style>
