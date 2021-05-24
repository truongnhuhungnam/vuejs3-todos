<template>
    <TheHeader />
    <div class="mx-auto py-4 w-1/2">
        <BaseTodos />
    </div>
</template>

<script>
import TheHeader from './components/TheHeader'
import BaseTodos from './components/Todos/BaseTodos'
export default {
    components: { TheHeader, BaseTodos },
}
</script>
