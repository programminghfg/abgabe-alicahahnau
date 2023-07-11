<script>
    import { onMount } from 'svelte';
    import { useParams } from 'svelte-routing';
    
    let cocktail = null;
  
    const { id } = useParams();
</script>