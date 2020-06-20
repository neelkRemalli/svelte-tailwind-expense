<script>
import Navbar from './components/Navbar.svelte'
import Title from './components/Title.svelte'
import ExpenseList from './components/ExpenseList.svelte'
import FormExpenses from './components/FormExpenses.svelte'
import Modal from './components/Modal.svelte'
import {onMount, afterUpdate} from 'svelte'

// import ExpensesData from './expenses'
let expenses = []

let setName = ''
let setAmount = null
let setId = null
let isFormOpen = false

 $:total = expenses.reduce((acc, curr)=>{ return (acc +=curr.amount)},0)
 $:isEditing = setId ? true : false

 const showForm = () =>{
	 isFormOpen = true
 }
 const hideForm = () =>{
	 isFormOpen = false
	 setName = ''
	 setAmount = null
	 setId = null
 }
const handleAddExpenses = ({name, amount}) =>{
let expense = { id: Math.random() * Date.now(), name, amount };
	expenses = [expense, ...expenses];	
}
const handleModifyExpenses = (e) =>{
	const id = e.detail
	const expense = expenses.find(item => item.id === id)
	setName = expense.name;
	setAmount = expense.amount;
	setId = expense.id;
	showForm()
}
const handleEditExpenses = ({name, amount}) =>{
	expenses = expenses.map(item => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setAmount = null;
	setName = "";
}

const handleDelete = (e) =>{
	const id = e.detail;
	expenses = expenses.filter(el => el.id !== id)		
}
const handleClear = ()=>{
	expenses = []  	
}

const setLocalStorage = () => {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }

  onMount(()=>{
	  expenses = localStorage.getItem('expenses')
	  ? JSON.parse(localStorage.getItem('expenses'))
	  : []
  })
  afterUpdate(()=>{
	setLocalStorage() 
  })
 

</script>

<Navbar {showForm} />
<main class=' max-w-xl w-4/5 mx-auto mt-6'>
	{#if isFormOpen}
	<Modal>
	<FormExpenses {handleAddExpenses} name={setName} amount={setAmount} {isEditing} {handleEditExpenses} {hideForm}  />
    </Modal>
	{/if}
	<Title title='total expenses' {total} />
	<ExpenseList {expenses}
	 on:delete={handleDelete}
	 on:click={handleClear} 
	 on:edit={handleModifyExpenses}
	  />

</main>


<style>
	
	:global(body){
		padding: 0;
		background: #eeeeee65;
		
	}
</style>