

<template>
  <div class="dashboard">
    <div class="dashboard-content">
      <h2>Welcome to VOTI</h2>
      <p class="lead">You can create ur own Event or check already existing ones</p>
      <p class="leadi">Have fun choosing which Events to vote for.</p>

      <div class="dashboard-actions">
        <b-card class="action-card">
          <div class="card-content">
            <h4>Create an Event</h4>
            <p>Create a new Event and share it's information with the community.</p>
            <router-link to="/create-discussion">
              <button variant="primary" class="action-btn">Create Event</button>
            </router-link>
          </div>
        </b-card>

        <b-card class="action-card">
          <div class="card-content">
            <h4>View Events</h4>
            <p>Browse existing Events and vote for your favourite.</p>
            <router-link to="/discussions">
              <button variant="secondary" class="action-btn">View Events</button>
            </router-link>
          </div>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
};
</script>

<style scoped>
.dashboard {
  background-color: #f8f9fa;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.dashboard-content {
  text-align: center;
  max-width: 800px;
  padding: 20px;
}

h2 {
  font-size: 3rem;
  color: #ff5e62;
  margin-bottom: 20px;
}

.lead {
  font-size: 1.25rem;
  color: #6c757d;
  margin-bottom: 40px;
}
.leadi {
  font-size: 1.25rem;
  font-weight: bold;
  color: #6c757d;
  margin-bottom: 40px;
}

.dashboard-actions {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.action-card {
  flex: 1;
  padding: 20px;
  border-radius: 10px;
  background-color: #ffffff;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.action-card:hover {
  transform: translateY(-10px);
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.2);
}

.card-content {
  text-align: center;
}

h4 {
  color: #343a40;
  margin-bottom: 10px;
}

p {
  color: #6c757d;
  margin-bottom: 20px;
}

.action-btn {
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #ff5e62;
  border-radius: 30px;
  text-decoration: none;
  color: white;
  text-decoration: none;
  
}






</style>

