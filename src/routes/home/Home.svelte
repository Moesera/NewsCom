<script>
  let country = "";
  let uniData = [];

  async function apiFetch() {
    try {
      const res = await fetch(
        `http://universities.hipolabs.com/search?country=${country}`,
      );

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
    <input
      bind:value={country}
      id="search"
      name="search"
      type="text"
      placeholder="Enter country"
    />

    <button type="submit">Search</button>
  </form>
</section>

<section class="resultSection"> 
  {#each uniData as uni }
    <div class="uniBoxResult">
      <h3>{uni.name}</h3>
      <a href="{uni.web_pages[0]}">{uni.web_pages[0]}</a>
      <span class="badge float-right">{uni.country}</span>
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

  input#search {
    background: #e5e5e5;
    border: none;
    border-radius: 3px;
    color: #4e4c4e;
    font-family: inherit;
    font-size: 14px;
    height: 40px;
    outline: none;
    padding: 0px 10px;
    width: 300px;
  }

  .badge {
    display: inline-block;
    padding: 0.25em 0.4em;
    font-size: 75%;
    font-weight: 700;
    line-height: 1;
    text-align: center;
    white-space: nowrap;
    vertical-align: baseline;
    border-radius: 0.25rem;
    color: #fff;
    background-color: #17a2b8;
  }

  .float-right {
    float: right;
  }

</style>
