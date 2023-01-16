
<script>
    let hello = () => alert("Hello");
    let hola = () => alert("Hola");
    let ola = () => alert("Olá");
</script>

<!-- Challenge: Handle the click event in the root page (/task-group-3/+page.svelte) and `alert("No, fuck you!")` there instead -->
<button on:click={() => alert("No, fuck you!")} type="button" class="text-white bg-gradient-to-r from-green-400 via-green-500 to-green-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-green-300 dark:focus:ring-green-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Fuck You</button>
<br><br>


<!-- 
    Challenge: Follow the directions by passing events up the layer chain

    Hint: You will need to use import and use `createEventDispatcher` to create 3 different events types, one for each button
-->
<div class="inline-flex rounded-md shadow-sm" role="group">
    <!-- Instead of handling the event here, pass the click event to LayerTwo and `alert("Hello")` there instead -->
    <button on:click={hello} type="button" class="px-4 py-2 text-sm font-medium text-gray-900 bg-white border border-gray-200 rounded-l-lg hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-gray-700 dark:border-gray-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white">
        Hello
    </button>
    <!-- Instead of handling the event here, pass the click event to LayerOne and `alert("Hola")` there instead -->
    <button on:click={hola} type="button" class="px-4 py-2 text-sm font-medium text-gray-900 bg-white border-t border-b border-gray-200 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-gray-700 dark:border-gray-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white">
        Hola
    </button>
    <!-- Instead of handling the event here, pass the click event to the root page (/task-group-3/+page.svelte) and `alert("Olá")` there instead -->
    <button on:click={ola} type="button" class="px-4 py-2 text-sm font-medium text-gray-900 bg-white border border-gray-200 rounded-r-md hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-gray-700 dark:border-gray-600 dark:text-white dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-blue-500 dark:focus:text-white">
        Olá
    </button>
</div>
