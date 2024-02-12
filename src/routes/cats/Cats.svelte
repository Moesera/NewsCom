<script>
    var catsUrl = "";
    var imgClass = "hidden";
    var catBtnTxt = "Get cat";

    async function catFetch() {
        var randomNumber = Math.floor(Math.random() * 1000);
        catsUrl = "https://cataas.com/cat?random=" + randomNumber;
        imgClass = "";
        catBtnTxt = "Get new cat";
    }
</script>

<h1>Cat picture generator</h1>

<p>Click the button to get a get image</p>

<section>
    <button on:click={catFetch}>{catBtnTxt}</button>
</section>

<section>
    <img src={catsUrl} alt="a cat" class={imgClass} />
</section>

<style>
    .hidden {
        display: none;
    }
</style>