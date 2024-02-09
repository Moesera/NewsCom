<script>
  let country = "";
  let uniData = [];

  async function apiFetch() {
    try {
      const res = await fetch(
        `http://universities.hipolabs.com/search?country=${country}`,
      );
      // alert(`this is ${country}`);

      uniData = await res.json();

      console.log(uniData);
    } catch (e) {
      console.log(e);
    }
  }
</script>

<h1>Uni search</h1>

<p>Search for country</p>

<section>
  <form method="POST" on:submit|preventDefault={apiFetch}>
    <!-- <label for="search" >search</label> -->
    <input
      bind:value={country}
      id="search"
      name="search"
      type="text"
      placeholder="search"
    />

    <button type="submit">Submit</button>
  </form>
</section>

<section class="resultSection">
  <h2>List of uni Results</h2>
{#each uniData as uni }
  <div class="uniBoxResult">
    <h3>{uni.name}</h3>
    <div>
      <h4>Webpage</h4>
      <p>{uni.web_pages[0]}</p>
    </div>
    <span>{uni.country}</span>
  </div>
{/each}
</section>

<style>
  form {
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }
  input {
    padding: 0.4rem;
    margin: 0rem;
  }

  .resultSection {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .uniBoxResult {
    background: rgba(120,102,240, 0.40);
    padding: 0.8rem;
    border-radius: 0.4rem;
  }
</style>
