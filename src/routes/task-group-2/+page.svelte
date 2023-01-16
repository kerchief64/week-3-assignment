<!-- Topics Covered -->
<!-- 
    - DOM Events
    - Inline Handlers
    - Event modifiers
-->
<script>
    // Executed when the image starts to be dragged
    function drag(event) {
        // Start a dataTransfer event with format and data as our arguments
        // Images are under the "text" category (for some reason)
        // The second argument "data", takes our target id

        // Note: dataTransfer.setData is take ownership of the image by ripping it out of its current div
        event.dataTransfer.setData("text", event.target.id);
    }
    
    // Executes when the image is dropped
    function drop(event) {
        // Get the image from the dataTransfer Object
        let data = event.dataTransfer.getData("text");

        // Append the image to the new div
        event.target.appendChild(document.getElementById(data));
    }

    // Needed to prevent a browser bug
    function allowDrop(event) {
        event.preventDefault();
    }
</script>

<div class="m-6">

    <h2 class=" text-4xl font-extrabold dark:text-white m-4">Rick Roll Drag & Drop</h2>

    <p class="m-4 text-lg font-normal text-gray-500 lg:text-xl dark:text-gray-400">
        You can drag this image back and forth between the boxes
    </p>
    
    <!-- 
        `ondrop` is using the vanilla html and javascript method to work.
        However, in Svelte using the vanilla method will break the application
    
        Challenge: Fix `div1` and `div2` so they use the Svelte DOM Event method instead
        Note: Drag and drop should work correctly if you do this the correct way
     -->
    <div id="div1" ondrop="drop(event)" on:dragover="{allowDrop}">
        <img src="https://svelte.dev/tutorial/image.gif" alt="Rick Roll" draggable="true" on:dragstart="{drag}" id="drag1">
    </div>
      <br>
    
    <!-- 
        Notice how the `allowDrop` function simple calls `event.preventDefault()`
        
        Challenge: Use a Event Modifier to do this instead.
    
        Note: In order for this to work, you still must give on:dragover a function to execute,
              try using a empty Inline Handler as a placeholder. 
              (Empty meaning it contains no event in the argument or executable code in the body)
     -->
    <div id="div2" ondrop="drop(event)" on:dragover="{allowDrop}"></div>    
</div>

<style>
	#div1, #div2 { 
        width: 400px; 
        height: 300px;
        padding: 20px;
        display: block;
        border-color: white;
        border-width: 3px;
        border-style: solid;
    }
</style>