<script>
    import LayerOne from "./LayerOne.svelte";

    let ola = () => alert('Olá');

    function handleMessage(event) {
        alert(event.detail.text)
    }
</script>

<div class="m-6">
    <h2 class="mb-12 text-4xl font-extrabold dark:text-white m-4">Nested Buttons</h2>
    <LayerOne on:click={() => alert("No, fuck you!")} on:ola={ola} on:message={handleMessage}/>
</div>