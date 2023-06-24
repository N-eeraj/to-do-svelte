<script>
let input = ''
let items = []

const handleKeyDown = ({key}) => {
  if (key === 'Enter')
    addItem()
}

const handleInput = ({target}) => input = target.value

const addItem = () => {
  items = [...items, {
    text: input,
    done: false
  }]
  input = ''
}

const clearList = () => items = []

const crossItem = index => items[index].done = true

const deleteItem = index => items = items.filter((_, i) => index !== i)
</script>

<div>
  <input type="text" placeholder="Enter Item Here" value={input} on:keydown={handleKeyDown} on:input={handleInput}>
  <button on:click={addItem}>Add Item</button>
  <button on:click={clearList}>Clear List</button>
</div>

<div id="item_list">
  {#each items as item, index}
    <div class={"item" + ((item.done)? " done":'')}>
      <i class="fa-solid fa-square-check" on:click={() => crossItem(index)}></i>
      <span on:click={() => crossItem(index)}>{item.text}</span>
      <i class="fa-solid fa-trash-can" on:click={() => deleteItem(index)}></i>
    </div>
  {/each}
</div>