<script>

    export let image="https://www.celio.com/medias/sys_master/productMedias/productMediasImport/h22/h6b/10120899035166/essentiel-le-t-shirt-slim-blanc-1061351-1-product.jpg";
    let width;
    let height;
    let size = 50;
    let top = 50;
    let left = 50;
    let text = 'Test';
    let color = 'red';

</script>
<div id="param">
<p>Taille:</p>
<input type=range min=0 max=700 bind:value={size}>
<p>Hauteur:</p>
<input type=range min=0 max=100 bind:value={top}>
<p>Largeur:</p>
<input type=range min=0 max=100 bind:value={left}>
<input bind:value={text}>

<p>size: {width}px x {height}px</p>
</div>

<div class="contenant">
    <img src={image}>
    <div style="top:{top}%; left:{left}%" class="texte_centrer" bind:clientWidth={width} bind:clientHeight={height}>
        <span style="color:{color} ; font-size: {size}px">{text}</span>
    </div>
</div>

<style>

    input {
        display: block;
    }
    div {
        display: inline-block;
    }
    .contenant {
        position: relative;
        text-align: center;
        color: red;
    }

    .texte_centrer {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
    #param{
        display: block;
        width: 50%;
        text-align: center;
    }
    input{
        margin: auto;
        align-items: center;

    }

</style>