<script>
    export let choices = 4;
    export let phraseUn = "Politique de confidentialité";
    export let phraseDeux = "cookies";
    export let phraseTrois = "Données personnels";
    export let phraseQuatre = "Majeur";
    let un = false;
    let deux = false;
    let trois = false;
    let quatre = false;
</script>

<div id="main">
    <label>
        {#if choices >= 1}
            <div class="inputChoice">
                <input type=checkbox bind:checked={un}>
                <span>{phraseUn}<span/>
            </div>
        {/if}

        {#if choices >= 2}
            <div class="inputChoice">
                <input type=checkbox bind:checked={deux}>
                <span>{phraseDeux}<span/>
            </div>
        {/if}

        {#if choices >= 3}
            <div class="inputChoice">
                <input  type=checkbox bind:checked={trois}>
                <span>{phraseTrois}<span/>
            </div>
        {/if}

        {#if choices == 4 }
            <div class="inputChoice">
                <input type=checkbox bind:checked={quatre}>
                <span>{phraseQuatre}<span/>
            </div>
        {/if}
    </label>




    {#if choices == 1}
        {#if un}
            <p>Merci, c'est validé.</p>
        {:else}
            <p>Cocher toutes les cases pour continuer.</p>
        {/if}
        <button disabled={!un}>Valider</button>
    {:else if choices == 2}
        {#if un && deux}
            <p>Merci, c'est validé.</p>
        {:else}
            <p>Cocher toutes les cases pour continuer.</p>
        {/if}
        <button disabled={!un || !deux}>Valider</button>
    {:else if choices == 3}
        {#if un && deux && trois}
            <p>Merci, c'est validé.</p>
        {:else}
            <p>Cocher toutes les cases pour continuear.</p>
        {/if}
        <button disabled={!un || !deux || !trois}>Valider</button>
    {:else}
        {#if un && deux && trois && quatre}
            <p>Merci, c'est validé.</p>
        {:else}
            <p>Cocher toutes les cases pour continuer.</p>
        {/if}
        <button disabled={!un || !deux || !trois || !quatre}>Valider</button>
    {/if}
</div>

<style>
    #main {
        height: 40%;
        width: 20%;
        margin: 50px;

        align-items: center;
        border-radius: 5%;
        box-shadow: 5px 5px 20px 0px gray;
        padding: 20px;
    }
    label{
        display: inline-grid;

    }
    .inputChoice{
        width: 100%;

        margin: 1em 0 1em 0;
        text-align: justify;
    }
    span, p{
        font-family: Arial;

    }
    p{
        font-weight: bold;
    }
</style>