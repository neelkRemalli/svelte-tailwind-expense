<script>
    import FaCaretDown from 'svelte-icons/fa/FaCaretDown.svelte'
    import FaPen from 'svelte-icons/fa/FaPen.svelte'
    import FaTrash from 'svelte-icons/fa/FaTrash.svelte'
    import {fade, blur, fly, scale, slide} from 'svelte/transition'
    
    import {createEventDispatcher} from 'svelte'

    const dispatch = createEventDispatcher(); 
    export let id;
    export let name ='';
    export let amount = 0;
    let isOpenAmount = false;
</script>

<article class="bg-orange-100 flex justify-between items-center sm:py-4 py-2 px-6 shadow-lg rounded-lg">
    <div class="w-1/2">
        <h2 class="flex items-center">
            <span class="sm:text-xl mr-4">{name}</span>
        <button class='inline-block h-3 w-3 text-blue-500 focus:outline-none' on:click={()=>(isOpenAmount = !isOpenAmount)}>
           <div >
            <FaCaretDown  />
           </div>
        </button>
    </h2>
    {#if isOpenAmount}
    <h2 class='text-blue-400 sm:text-xl mt-4' transition:slide>Amount : ${amount}</h2>
    {/if}
    </div>
    <div>
        <button class='inline-block h-4 w-4 mr-3 text-green-700 focus:outline-none'
        on:click={()=>dispatch('edit', id)}
        >
       <div class='transform hover:scale-110 transition duration-500 '>
        <FaPen />
       </div>
        </button>
        <button class='inline-block h-4 w-4 text-red-600 focus:outline-none'>
         <div class='transform hover:scale-110 transition duration-500'
           on:click={()=>dispatch('delete', id)}
         >
            <FaTrash />
         </div>
        </button>
    </div>
</article>


<style>
    
</style>