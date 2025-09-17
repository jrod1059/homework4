<script setup>
    import {defineProps} from 'vue'
    
    const props = defineProps({
        income: {
            type: Number,
            require: true,

        },
        expense: {
            type: Number,
            require: true,
        }
    })

</script>

<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="Money-plus" class="money plus">+${{ income }}</p>
        </div>

        <div>
            <h4>Expense</h4>
            <p id="Money-minus" class="money minus">-${{ expense }}</p>
        </div>
    </div>


</template>