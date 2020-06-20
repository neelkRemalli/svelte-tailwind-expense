<script>
    import FaTimes from 'svelte-icons/fa/FaTimes.svelte'
    export let handleAddExpenses
    export let handleEditExpenses
    export let name = ''
    export let amount = null
    export let isEditing
    export let hideForm
   
  
    $: isEmpty = !name || !amount;

   const handleSubmit = () =>{
       if(isEditing){
           handleEditExpenses({name, amount})
        }else{
            handleAddExpenses({name, amount})
       }
       hideForm()
    name = ''
    amount = null
    }
</script>

<div class="relative bg-white sm:p-12 p-3 rounded-lg z-10">
    
        <h3 class='text-blue-500 sm:text-2xl font-semibold mb-6 '> Add Expense</h3>
    <form on:submit|preventDefault={handleSubmit}>
        <div >
            <label for='name' class='block sm:text-lg'>name:</label>
            <input type='text' id='name' bind:value={name} class='w-full p-1 border-b border-blue-500 my-1 focus:outline-none'>
        </div>
        <div>
            <label for="amount" class='block sm:text-lg '>Amount:</label>
            <input type='number' id="amount" bind:value={amount} class=' w-full p-1 border-b border-blue-500 my-1 focus:outline-none'>
        </div>
        {#if isEmpty}
        <p class='text-center mt-1 sm:text-lg text-sm text-red-500'>please fill out all form fields</p>
        {/if}
        <button type='submit' class='bg-transparent border border-blue-500 block w-full p-1 inline-block my-5
         focus:outline-none text-blue-500 hover:bg-blue-500 hover:text-white rounded capitalize animation duration-500'
         disabled={isEmpty}
         class:disabled={isEmpty}
         >
         {#if isEditing}edit expense {:else}add expenses{/if}
        </button>
        <button type="button" class="inline-block flex items-center  w-20 absolute text-red-500 top-0 right-0 sm:p-2 font-semibold focus:outline-none"
         on:click={hideForm}
        >
            <div class='h-4 w-4 inline-block '>
                <FaTimes />
            </div>
            <span class="sm:ml-1">
                close
            </span>
           
        </button>
    </form>
   
</div>


<style>
    .disabled{
          opacity: 0.65; 
          cursor: not-allowed;
          background-color: transparent;
          color: gray;
           } 
    
</style>