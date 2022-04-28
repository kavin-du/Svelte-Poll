<script>
  export let type = "primary";
  export let flat = false;
  export let inverse = false;
</script>

<!-- conditional classes, only apply class flat, if flat is true -->
<button class={type} class:flat={flat} class:inverse={inverse} on:click>
  <slot />
</button>

<style>
  button {
    border: 0;
    cursor: pointer;
    border-radius: 8px 12px;
    padding: 8px 12px;
    font-weight: bold;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
  }
  .primary {
    background: tomato;
    color: white;
  }
  .secondary {
    background: teal;
    color: white;
  }
  .flat {
    box-shadow: none;
  }
  
  .primary.inverse {
    color: tomato;
    background: white;
    border: 2px solid tomato; 
  }
  .secondary.inverse {
    color: teal;
    background: white;
    border: 2px solid teal;
  }
</style>
