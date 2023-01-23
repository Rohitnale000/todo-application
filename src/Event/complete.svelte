<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()
</script>

<a href="#" class="isCompleted" on:click={()=> dispatch("message",{iCnt:2})}>Completed</a>
