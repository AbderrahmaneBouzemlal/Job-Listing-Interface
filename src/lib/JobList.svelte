<script>
  import { jobs } from './jobs';
  import JobCard from './JobCard.svelte';
  import { selectedFilters } from './store.svelte.js';

  let filteredJobs = $derived.by(() => {
    if (selectedFilters.value.length === 0) {
      return jobs;
    }
    return jobs.filter((job) => {
      const jobTags = [job.role, job.level, ...job.languages, ...job.tools];
      return selectedFilters.value.every((filter) => jobTags.includes(filter));
    });
  });

  function removeFilter(filter) {
    selectedFilters.value = selectedFilters.value.filter((f) => f !== filter);
  }
</script>

<div class="relative flex flex-col gap-6 mb-12">
  {#if selectedFilters.value.length > 0}
    <div
      class="absolute -top-36 z-10 bg-white flex flex-wrap justify-between items-center w-full h-20 px-8 py-6 rounded-md shadow-md"
    >
      <div class="flex flex-wrap">
        {#each selectedFilters.value as filter, index}
          <span
            class="bg-background-green-50 text-primary-green-400 font-bold p-1 hover:cursor-pointer ml-3"
          >
            {filter}
          </span>
          <button
            onclick={() => {
              removeFilter(filter);
            }}
            class="bg-primary-green-400 hover:text-white p-1 hover:bg-green-900 hover:cursor-pointer"
          >
            <img src="/images/icon-remove.svg" alt="remove" />
          </button>
        {/each}
      </div>
      <button
        class="text-green-900 hover:underline hover:text-primary-green-400 hover:cursor-pointer mr-3"
        onclick={() => (selectedFilters.value = [])}
      >
        clear
      </button>
    </div>
  {/if}

  {#each filteredJobs.length === 0 ? jobs : filteredJobs as job, index}
    <JobCard {job} {index} />
  {/each}
</div>

{#if jobs.length === 0}
  <div class="text-center py-12 animate-fade-in">
    <div
      class="w-16 h-16 text-green-900 rounded-full flex items-center justify-center mx-auto mb-4"
    >
      <svg
        class="w-8 h-8"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M9 12h6m-6 4h6m2-10h.01M9 16h.01M9 8h.01M15 8h.01M21 12c0 4.418-4.035 8-9 8a9.863 9.863 0 01-3.95-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.035-8 9-8s9 3.582 9 8z"
        ></path>
      </svg>
    </div>
    <h3 class="text-xl text-primary-green-400 font-semibold mb-2">No job found</h3>
  </div>
{/if}
