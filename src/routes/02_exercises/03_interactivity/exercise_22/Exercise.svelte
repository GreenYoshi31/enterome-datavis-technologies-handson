<script>
    let num_clicks = 0;
    function click(event) {
        num_clicks = num_clicks + 1;
    }
    function reset(event) {
        num_clicks = 0;
    }
</script>

<button type="button" class="btn btn-danger" on:click={reset}>Reset</button>
<button type="button" class="btn btn-success" on:click={click}>{num_clicks}</button>