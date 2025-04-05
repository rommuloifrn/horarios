<script>
    let { children } = $props();
    import "../app.css";
</script>

<div class="p-3 ">
    {@render children()}
</div>