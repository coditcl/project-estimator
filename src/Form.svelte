<script>
import materialStore from './material-store.js';
export let id;
export let name = "";
export let price;



$: mode = id ? "edit" : "add";

$: canSubmit = price >= 0 && name !== "";

function submit(){
    if(!canSubmit){
        return
    }
    price = '';
    name = '';
    id = undefined;
}

if(mode === 'add'){
materialStore.add(name, price);

}

function cancel(){
    price = '';
    name = '';
    id = undefined;
}

</script>

<form on:submit|preventDefault={submit}>
 <fieldset>
  <label for="nameField
  ">Material</label>
  <input type="text" id="nameField" bind:value={name} placeholder="Wood, Glue, Etc.">

   <label for="priceField
  ">Price</label>
  <input type="number" min="0" step="any" bind:value={price} id="priceField" placeholder="Price">
 </fieldset>
 <button disabled={!canSubmit} class="float-right" type="submit">{mode}</button>
 {#if mode === 'edit'}
 <button on:click={cancel} class="float-right" type="button">Cancel</button>
 {/if}
</form>


<style>
button{
    margin-left:20px;
}
button:disabled{
    cursor: not-allowed;
}
</style>