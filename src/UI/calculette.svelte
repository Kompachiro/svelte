<main>


</main>

<script>
    let a = 1
    let b = 2
</script>

<div class ="chiffre">
    <input  type=number value={a} min=0 max=100>
    <input type=range bind:value={a} min=0 max=100>
</div>

<div class ="chiffre2">
    <input  type=number value={b} min=0 max=100>
    <input type=range bind:value={b} min=0 max=100>
</div>

<p> {a}cm + {b}kg = {a/10.23 + b/1.2} € </p>




<style>
    .texte1 {

    }
    .texte1:hover {
        filter: drop-shadow(0 0 2em rgba(237, 237, 237, 0.667));
    }

    .chiffre {
        padding: 0;
        margin: 0;
        list-style: none;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    input {
        margin: 10px
    }

    .chiffre2 {
        padding: 0;
        margin: 0;
        list-style: none;
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>