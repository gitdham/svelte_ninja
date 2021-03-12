<script>
  // declare props
  export let showModal = false;
  export let message = "default value";
  export let isPromo = false;
</script>

{#if showModal}
  <!-- set class promo if isPromo is true -->
  <!-- on:click event forwarding -->
  <!-- self: event modifiers. only fires the event if the clicked element is the target -->
  <div class="backdrop" class:promo={isPromo} on:click|self>
    <div class="modal">
      <p>{message}</p>
    </div>
  </div>
{/if}

<style>
  .backdrop {
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
  }
  .modal {
    padding: 10px;
    border-radius: 10px;
    max-width: 400px;
    margin: 10% auto;
    text-align: center;
    background: #fff;
  }

  .promo .modal {
    background: crimson;
    color: #fff;
  }
</style>
