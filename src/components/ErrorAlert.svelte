<script lang="ts">
  export let error: Error
</script>

<div class="col-12 text-center">
  <div class="animate__animated animate__jello alert alert-danger">
    {error.message}
  </div>
</div>
