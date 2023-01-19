<script>
    import LayerTwo from "./LayerTwo.svelte";

    let hola = () => alert('Hola');
</script>

<LayerTwo on:click on:ola on:hola={hola}/>