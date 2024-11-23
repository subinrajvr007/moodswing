<script>
  import { negativeScenarios, positiveResponses } from './lib/moodData.js';
  
  let selectedScenario = null;
  let showResponse = false;
  let response = '';
  
  function handleSelect(scenario) {
    selectedScenario = scenario;
    showResponse = false;
  }
  
  function swingMood() {
    const index = negativeScenarios.indexOf(selectedScenario);
    response = positiveResponses[index];
    showResponse = true;
  }
</script>

<main class="container py-4">
  <div class="mood-card card">
    <div class="card-header bg-primary text-white">
      <h1 class="h3 mb-0 text-center">MoodSwing</h1>
    </div>
    <div class="card-body">
      <h5 class="card-title text-center mb-4">What's bringing you down?</h5>
      <div class="list-group">
        {#each negativeScenarios as scenario}
          <button
            class="list-group-item list-group-item-action {selectedScenario === scenario ? 'active' : ''}"
            on:click={() => handleSelect(scenario)}
          >
            {scenario}
          </button>
        {/each}
      </div>
      
      <div class="text-center mt-4">
        <button
          class="btn btn-success btn-lg"
          disabled={!selectedScenario}
          on:click={swingMood}
        >
          Swing my mood!
        </button>
      </div>
    </div>
  </div>

  {#if showResponse}
    <div class="response-card card {showResponse ? 'show' : 'hide'} bg-light">
      <div class="card-body">
        <h5 class="card-title text-center text-success">Look on the bright side...</h5>
        <p class="card-text text-center lead">{response}</p>
      </div>
    </div>
  {/if}
</main>