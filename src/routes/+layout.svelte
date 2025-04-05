<script>
    let { children } = $props();
    import "../app.css";
</script>

<div class="p-3 flex justify-center">
    <main>
        {@render children()}
    </main>
</div>