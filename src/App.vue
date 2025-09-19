<script setup>
    import Header from './components/Header.vue';
    import Balance from './components/Balance.vue';
    import IncomeExpenses from './components/IncomeExpenses.vue';
    import AddTransactions from './components/AddTransactions.vue';
    import TransactionList from './components/TransactionList.vue';
    import {ref, computed} from 'vue'

    const transactions = ref([])

    const sum = computed(()=>{
        return transactions.value.reduce((acc, x)=>{
            return acc+x.amount
        },0)
    })

    
    const moneyIn = computed(()=>{
        return transactions.value
        .filter((x)=>x.amount>0)
        .reduce((acc, x)=>{
            return acc+x.amount
        },0)
    })

    const moneyOut = computed(()=>{
        return transactions.value
        .filter((x)=>x.amount<0)
        .reduce((acc, x)=>{
            return acc+x.amount
        },0)
    })


    const handleTransaction =(transactionData) => {
        transactions.value.push({
            id: generateID(),
            text: transactionData.text,
            amount: transactionData.amount,
        }
        )
    }

    const generateID = () => {
        return Math.floor(Math.random()*10000000)
    }

    const handleDelete = (id) => {
        transactions.value = transactions.value.filter((x) => x.id !== id)
    }


</script>

<template>
    <Header></Header>
    <div class="container">
        <Balance :total = "sum"></Balance>
        <IncomeExpenses :income="moneyIn" :expense="-moneyOut"></IncomeExpenses>
        <AddTransactions @transaction-submitted="handleTransaction"></AddTransactions>
        <TransactionList :transactions="transactions" @transaction-deleted="handleDelete"></TransactionList>
    </div>


</template>