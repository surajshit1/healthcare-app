<script>
  export let services = [];
  export let deleteService;
  export let editService;
</script>

<div class="row">
  {#each services as service}
    <div class="col-md-12 mb-4">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">{service.name}</h5>
          <p class="card-text">{service.description}</p>
          <p class="card-text"><strong>Price: </strong>${service.price}</p>
          <button class="btn btn-success mr-2" on:click={() => editService(service)}>Edit</button>
          <button class="btn btn-danger" on:click={() => deleteService(service.id)}>Delete</button>
        </div>
      </div>
    </div>
  {/each}
</div>

<style>
  .card {
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .btn {
    margin-top: 10px;
  }
</style>
