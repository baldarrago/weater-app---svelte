<script lang="ts">
  import { createEventDispatcher } from "svelte"

  export let city: string = ""

  const dispatch = createEventDispatcher()

  const handleSubmit = () => {
    dispatch("handleSubmit", city)
    city = ""
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  <label class="form-label">
    City: <input bind:value={city} type="text" class="form-control" />
  </label>
  <button class="btn btn-info">Search</button>
</form>
