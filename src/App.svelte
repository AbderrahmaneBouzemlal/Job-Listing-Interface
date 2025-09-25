<script>
  import Header from './lib/Header.svelte';
  import JobList from './lib/JobList.svelte';
  import { setContext } from 'svelte';
</script>

<div class=" bg-background-green-50 min-h-screen">
  <header>
    <Header></Header>
  </header>
  <main class="max-w-6xl mx-auto -mt-20 p-4">
    <JobList></JobList>
  </main>
</div>
