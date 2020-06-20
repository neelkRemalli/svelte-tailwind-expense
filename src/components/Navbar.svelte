<script>
    import FaRegPlusSquare from 'svelte-icons/fa/FaRegPlusSquare.svelte'
    export let showForm
</script>
<nav class=' flex items-center bg-blue-500 p-6 sm:text-2xl shadow-lg'>
    <div class='flex w-full sm:max-w-xl w-4/5 items-center justify-between mx-auto'>
        <h1 class='text-blue-100 font-semibold tracking-wide'>Budget Calculator</h1>
        <h1 >
            <button class='flex items-center inline-block text-blue-100 tracking-tighter focus:outline-none' type='button' on:click={showForm}>
                <span class='inline-block w-4 h-4 sm:w-6 sm:h-6 text-blue-100'>
                    <FaRegPlusSquare />
                </span>
                Add item
            </button>
        </h1>
    </div>
</nav>


<style>
   
</style>