<script>
  // @ts-nocheck
  import { getContext } from 'svelte';
  import { selectedFilters } from './store.svelte.js';

  let { job, index = 0 } = $props();

  function select(addedFilter) {
    selectedFilters.value.push(addedFilter);
    selectedFilters.value = Array.from(new Set(selectedFilters.value));
    console.log(selectedFilters.value.length);
  }
</script>

<div
  class="bg-white glass shadow-primary-green-400 shadow-lg backdrop-blur-sm p-6 rounded-md flex flex-col sm:flex-row justify-between items-start sm:items-center border-l-4 {job.featured
    ? 'border-primary-green-400'
    : 'border-transparent'} {index === 0 ? 'mt-0' : 'mt-6'}"
>
  <div
    class="relative md:static flex flex-col md:flex-row md:items-center md:justify-center lg:justify-between gap-4 w-full"
  >
    <img
      src={job.logo}
      alt={job.company}
      class="absolute -top-5 left-0 md:static h-12 w-12 -mt-6 mb-4"
    />
    <div class="flex flex-col py-5 md:flex-row justify-between md:items-start w-full ml-4">
      <div>
        <div class="flex md:items-center gap-4">
          <h3 class="text-primary-green-400 font-bold">{job.company}</h3>
          {#if job.new}
            <span
              class="text-xs text-white bg-primary-green-400 font-bold px-2 py-1 rounded-full mr-1"
              >NEW!</span
            >
          {/if}
          {#if job.featured}
            <span class="text-xs text-white bg-green-900 font-bold px-2 py-1 rounded-full"
              >FEATURED</span
            >
          {/if}
        </div>
        <h2 class="font-bold text-lg my-2 hover:text-primary-green-400 cursor-pointer">
          {job.position}
        </h2>
        <div class="text-gray-400 mb-2">
          <span>{job.postedAt}</span>
          <span class="mx-2">•</span>
          <span>{job.contract}</span>
          <span class="mx-2">•</span>
          <span>{job.location}</span>
        </div>
      </div>
      <div
        class="flex flex-wrap gap-4 mt-4 sm:mt-0 border-t border-gray-200 pt-4 sm:pt-0 sm:border-0"
      >
        <button
          class="bg-background-green-50 text-primary-green-400 font-bold p-1 hover:cursor-pointer hover:bg-primary-green-400 hover:text-white"
          onclick={() => select(job.role)}
        >
          {job.role}
        </button>
        <button
          class="bg-background-green-50 text-primary-green-400 font-bold p-1 hover:cursor-pointer hover:bg-primary-green-400 hover:text-white"
          onclick={() => select(job.level)}
        >
          {job.level}
        </button>
        {#each job.languages as language}
          <button
            class="bg-background-green-50 text-primary-green-400 font-bold p-1 hover:cursor-pointer hover:bg-primary-green-400 hover:text-white"
            onclick={() => select(language)}
          >
            {language}
          </button>
        {/each}
        {#each job.tools as tool}
          <button
            class="bg-background-green-50 text-primary-green-400 font-bold p-1 hover:cursor-pointer hover:bg-primary-green-400 hover:text-white"
            onclick={() => select(tool)}
          >
            {tool}
          </button>
        {/each}
      </div>
    </div>
  </div>
</div>
