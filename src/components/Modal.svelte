<script>
  import {fade, fly, blur} from 'svelte/transition'
</script>

<div class='bg-black fixed inset-0 z-10 modal' in:blur out:fade>
    <div class='bg-white w-10/12 md:max-w-lg md:max-w-xl mx-auto mt-24 p-1 rounded-lg relative'
    transition:fly={{y:200, delay: 400}}
    
    >
       <slot/>
    </div>
</div>

<style>
    .modal{
        background: rgba(0, 0, 0, 0.7);
    }
</style>