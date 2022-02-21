<template>
    <button
        class="bg-slate-100 hover:bg-slate-300 py-5 rounded-2xl active:translate-y-1 font-mono font-bold text-3xl"
    >{{number}}</button>
</template>

<script>
export default {
    props:['number'],
    setup(){

    }
}
</script>