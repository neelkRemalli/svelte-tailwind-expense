<script>
import ExpenseItem from './ExpenseItem.svelte'
import {fly} from 'svelte/transition'
import {flip} from 'svelte/animate'
export let expenses = []

</script>

{#each expenses as expense, index (expense.id)}
<div class="my-6 capitalize" in:fly={{x:200, delay: (index + 1)* 100}} out:fly={{x:-200}} animate:flip>
    <ExpenseItem {...expense} on:delete on:edit/>
</div>
 {:else}
 <h3 class='capitalize text-gray-600 sm:text-xl'>No expenses added to list</h3>
{/each}
<button class='bg-blue-500 p-2 block w-full rounded sm:text-lg text-white tracking-wide mt-12 font-semibold
 hover:bg-transparent border border-blue-500 hover:text-blue-500 animation duration-500 focus:outline-none'
 on:click
 >Clear Expenses</button>


