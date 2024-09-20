<script>
  export let addService;
  export let updateService;
  export let selectedService = null;

  let name = '';
  let description = '';
  let price = '';

  $: if (selectedService) {
    name = selectedService.name;
    description = selectedService.description;
    price = selectedService.price;
  }

  function handleSubmit() {
    if (name && description && price) {
      const service = { name, description, price: parseFloat(price) };
      if (selectedService) {
        updateService({ ...selectedService, ...service });
      } else {
        addService(service);
      }
      resetForm();
    } else {
      alert("All fields are required.");
    }
  }

  function resetForm() {
    name = '';
    description = '';
    price = '';
    selectedService = null;
  }
</script>

<form on:submit|preventDefault={handleSubmit} class="card p-4">
  <div class="form-group mb-3">
    <label for="name">Service Name</label>
    <input type="text" id="name" class="form-control" bind:value={name} placeholder="Service Name" />
  </div>

  <div class="form-group mb-3">
    <label for="description">Description</label>
    <textarea id="description" class="form-control" bind:value={description} placeholder="Description"></textarea>
  </div>

  <div class="form-group mb-3">
    <label for="price">Price</label>
    <input type="number" id="price" class="form-control" bind:value={price} placeholder="Price" />
  </div>

  <button type="submit" class="btn btn-primary btn-block">
    {selectedService ? 'Update Service' : 'Add Service'}
  </button>
</form>

<style>
  form {
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  button {
    margin-top: 10px;
  }
</style>
