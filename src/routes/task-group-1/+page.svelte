<!-- Topics Covered -->
<!-- 
    - OOP Programming Basics (A simple review)
    - Rerendering arrays / objects (Covered in the past)
    - Each block (Covered in the past)
    - Reactive statements
-->
<script>
    import { error } from '@sveltejs/kit';

    // A list of all the classes in Black Desert
    let characterClassesDisplay = [
        "Archer",
        "Berserker",
        "Corsair",
        "Dark Knight",
        "Drakania",
        "Guardian",
        "Hashashin",
        "Kunoichi",
        "Lahn",
        "Maehwa",
        "Musa",
        "Mystic",
        "Ninja",
        "Nova",
        "Ranger",
        "Sage",
        "Shai",
        "Sorceress",
        "Striker",
        "Tamer",
        "Valkyrie",
        "Warrior",
        "Wizard",
    ];

    class Character {
        constructor(characterName, characterClass, characterLevel) {
            // Some "hacky" parameter type checks, since we aren't using TypeScript
            if (typeof characterName !== 'string') 
                throw error(500, { message: 'Tried to add incorrect type to Character Object: characterName'});
            if (typeof characterClass !== 'string') 
                throw error(500, { message: 'Tried to add incorrect type to Character Object: characterClass'});
            if (typeof characterLevel !== 'number')
                throw error(500, { message: 'Tried to add incorrect type to Character Object: characterLevel'});

            this.name = characterName
            this.class = characterClass
            

            if (characterLevel != -1) this.level = characterLevel
            else this.level = ""

            // This will be used to check the objects type later on
            this.type = "character"
        }

        // Creates a placeholder version of it's self
        // Static means it can be used without creating an instance of it'self first using the "new" keyword
        static placeholder() {
            // -1 turns into a blank string as you can see the constructor method
            return new Character("", "", -1)
        }

        // Check if this instance of the Character Class is an empty placeholder
        isPlaceholder() {
            if (this.name === "" && this.class === "" && this.level === "") return true
            else return false
        }
    }

    class CharacterSheet {
        // Runs when the Object is created
        // No parameters in this case
        constructor() {
            this.characters = []
        }

        // Add a Character Object to this CharacterSheet Instance 
        addCharacter(character) {
            // Check to see if the parameter we put in is a "character" object. 
            // This is a "hacky" way of doing it since we aren't using TypeScript
            if (character.type === "character")
                // Push to our array of characters
                this.characters.push(character)
            else throw error(500, { message: 'Tried to add incorrect type to CharacterSheet Object'});
        }
    }

    // characterSheet is an Object that contains a array of individual Character Objects
    let characterSheet = new CharacterSheet();

    // This adds a blank place holder for the table
    characterSheet.addCharacter(Character.placeholder())

    // This function is called to force rerender the table of characters
    function updateCharacterSheet() {
        // We know that reactivity in svelte only happens when a variable is reassigned
        // Arrays and Objects both have interior mutability, meaning you can change them without reassigning them

        // Challenge: Force an update of characterSheet using 1 line of code below. 
        // DO NOT change anything else in the code to achieve this particular task

        // Hint: It's easier than you think and involves no functions or methods
 
    }

    // This Reactive statement checks if
    // 1: The first character is a placeholder
    // 2: If there is more than 1 entry in the table
    $: if(characterSheet.characters[0].isPlaceholder() && characterSheet.characters.length > 1) {
            // Challenge: Remove the placeholder using the .splice() function 
            
            updateCharacterSheet()
    }

    // Use the single line reactive statement below
    // Challenge: console.log() the amount of characters Objects in characterSheet
    // Hint: This should match the amount of rows your table has, including the initial placeholder table
    $: console.log("")
    
    $: {
        // Here we grab the array index of the newest character in the sheet
        let newestCharacter = characterSheet.characters.length - 1

        // Challenge: Use an if statement to check if the newest character is NOT a placeholder
        // If not a place holder, write 3 console.log statements that print the
        // Name, class, and level of that character, respectively

        // Hint: You should use the built-in isPlaceholder() method in your if statement

    }

    function addCharacterHandler(event) {
        // Challenge: Grab the need values below using the event variable
        let characterName = ""
        let characterClass = ""
        let characterLevel = 99

        characterSheet.addCharacter(new Character(characterName, characterClass, characterLevel))
        
        updateCharacterSheet()

        console.log(characterSheet.characters)
        document.getElementById("main-form").reset()
    }

</script>

<div class="m-6">
    <h2 class="mb-12 text-4xl font-extrabold dark:text-white m-4">Black Desert Character Sheet</h2>
 

    <h3 class="text-2xl font-extrabold dark:text-white mt-4 mb-4 text-center">My Characters</h3>
    <div class="relative overflow-x-auto">
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead class="text-center text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                <tr>
                    <th scope="col" class="px-6 py-3">
                        Name
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Class
                    </th>
                    <th scope="col" class="px-6 py-3">
                        Level
                    </th>
                </tr>
            </thead>
            <tbody class="text-center">
                <!-- Table Content -->
                {#each characterSheet.characters as character}
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                    <th scope="row" class="px-1 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        {character.name}
                    </th>
                    <td class="px-1 py-4">
                        {character.class}
                    </td>
                    <td class="px-1 py-4">
                        {character.level}
                    </td>
                </tr>
                {/each}
            </tbody>
        </table>
    </div>

    <br><br>

    <h3 class="text-2xl font-extrabold dark:text-white m-4 ml-0">Add a Character</h3>
    <form on:submit|preventDefault={addCharacterHandler} id="main-form">
        <div class="mb-6">
            <label for="character-class" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Character Name</label>
            <input type="text" id="character-class" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required>
        </div>

        <div class="mb-6">
            <label for="character-class" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Choose Class</label>
            <select id="character-class" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                {#each characterClassesDisplay as characterClass}
                    <option value="{characterClass}">{characterClass}</option>
                {/each}
            </select>
        </div>

        <div class="mb-6">
            <label for="character-level" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Character Level</label>
            <input type="number" min="1" value="1" id="character-level" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required>
        </div>


        <input type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
    </form>
</div>


