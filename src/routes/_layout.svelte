<script>
	
</script>

<style>
	:global(*){
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }
  :global(:root){
    --color-white:  #f0f2f5;
    --color-black: #1a1a1a;
    --color-primary: #ff3e00;

    --size-1: .75rem;
    --size-15: 1.125rem; 
    --size-2: 1.5rem;
    --size-25: 1.875rem;
    --size-3: 2.25rem;

    --box-shadow: -1px 1px 3px rgba(26,26,26,.15);
  }
</style>

<main>
	<slot></slot>
</main>