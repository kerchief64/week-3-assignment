<script>
    import ButtonGroup from "./ButtonGroup.svelte";

    let hello = () => alert('Hello');
</script>

<ButtonGroup on:click on:hola on:ola on:hello={hello}/>