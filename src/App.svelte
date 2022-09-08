<script>
    import CheckBox from './UI/checkBox.svelte';
    import Size from './UI/size.svelte';
    import Clock from './UI/Clock.svelte';
    import Color from './UI/color.svelte';
    import Dragdrop from './UI/dragdrop.svelte';
    import Carrousel from './UI/carrousel.svelte';
    import Video from './UI/videoPlayer.svelte';
    import Calculette from './UI/calculette.svelte';
    import Todo from './UI/todo.svelte';

    const test=4;
</script>

<h1 id="firstH">Checkbox</h1>
<div id="elementUn">
    <CheckBox
        choices={test}

        phraseQuatre="Majeur"
    />
</div>

<h1> Flockage logo</h1>
<div id="elementDeux">
    <Size
            image="https://www.celio.com/medias/sys_master/productMedias/productMediasImport/h22/h6b/10120899035166/essentiel-le-t-shirt-slim-blanc-1061351-1-product.jpg";
    />
</div>

<h1> Carrousel</h1>
<div>
    <Carrousel
    msecond="500"
    />

</div>

<h1>Clock</h1>
<div>
    <Clock type="black"/>

</div>

<h1>Color</h1>
<div>
    <Color/>

</div>
<h1>Dragdrop</h1>
<div>
    <Dragdrop/>
</div>
<h1>Lecteur vidéo</h1>
<div>
    <Video
            src='/kamp-koral-panique-chez-les-anchois.mp4';
            color="#fff"
    />
</div>

<h1>Frais de port</h1>
<div>
    <Calculette/>
</div>

<h1>Todo</h1>
<div>
    <Todo/>
</div>

<style>
    h1{
        font-family: sans-serif;
        border-top: solid;
        padding-top: 5%;
        text-align: center;
        margin-top: 5%;
    }
    #firstH{
        border-top: none;
        padding-top: 0;

    }
    #elementUn{
        text-align: center;
        align-items: center;
        align-content: center;
        display: flex;
        justify-content: center;
    }
    #elementDeux{
        display: flex;
        justify-content: center;

    }
    div{
        text-align: center;
    }

</style>