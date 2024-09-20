<script>
  import ServiceForm from './ServiceForm.svelte';
  import ServiceList from './ServiceList.svelte';

  let services = [
    { id: 1, name: 'General Checkup', description: 'Routine checkup', price: 50 },
    { id: 2, name: 'Blood Test', description: 'Basic blood test', price: 30 }
  ];
  let selectedService = null;
  let theme = localStorage.getItem('theme') || 'light';

  function addService(service) {
    services = [...services, { ...service, id: services.length + 1 }];
  }

  function deleteService(id) {
    services = services.filter(service => service.id !== id);
  }

  function updateService(updatedService) {
    services = services.map(service =>
      service.id === updatedService.id ? updatedService : service
    );
    selectedService = null;
  }

  function editService(service) {
    selectedService = { ...service };
  }

  function toggleTheme() {
    theme = theme === 'light' ? 'dark' : 'light';
    localStorage.setItem('theme', theme);
  }
</script>

<div class="container mt-5 {theme}">
  <h1 class="text-center mb-5">Healthcare Services</h1>


  <div class="theme-toggle mb-4 d-flex justify-content-end">
    <label class="switch">
      <input type="checkbox" on:change={toggleTheme} checked={theme === 'dark'}>
      <span class="slider round"></span>
    </label>
  </div>

  <div class="row">
    <div class="col-md-6 mb-4">
      <ServiceForm {addService} {selectedService} {updateService} theme={theme} />
    </div>
    <div class="col-md-6">
      <ServiceList {services} {deleteService} {editService} theme={theme} />
    </div>
  </div>
</div>

<style>
  .container.light {
    background-color: #f8f9fa;
    color: #000;
  }

  .container.dark {
    background-color: #343a40;
    color: #fff;
  }

  
  .switch {
    position: relative;
    display: inline-block;
    width: 50px;
    height: 24px;
  }

  .switch input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    transition: 0.4s;
    border-radius: 24px;
  }

  .slider:before {
    position: absolute;
    content: '';
    height: 18px;
    width: 18px;
    left: 4px;
    bottom: 3px;
    background-color: white;
    transition: 0.4s;
    border-radius: 50%;
  }

  input:checked + .slider {
    background-color: #2196F3;
  }

  input:checked + .slider:before {
    transform: translateX(24px);
  }
</style>
