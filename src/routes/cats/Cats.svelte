<script>
  import Button from '../../lib/components/page/Button.svelte';
  let catsUrl = '';
  let imgClass = 'hidden';
  let catBtnTxt = 'Get cat';

  async function catFetch() {
    var randomNumber = Math.floor(Math.random() * 1000);
    catsUrl = 'https://cataas.com/cat?random=' + randomNumber;
    imgClass = '';
    catBtnTxt = 'Get new cat';
  }
</script>

<h1>Cat picture generator</h1>

<p>Click the button to get a get image</p>

<section>
  <Button on:click={catFetch} buttonText={catBtnTxt}></Button>
</section>

<section>
  <img src={catsUrl} alt="a cat" class={imgClass} />
</section>

<style>
</style>
