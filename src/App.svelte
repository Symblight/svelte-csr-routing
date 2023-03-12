<script>
  import { path, query, fragment, pattern, click } from "svelte-pathfinder";

  import HomePage from "./pages/Home.svelte";
  import ProfilePage from "./pages/Profile.svelte";
  import PostPage from "./pages/Post.svelte";
  import PostsPage from "./pages/Posts.svelte";

  let params;
</script>

<svelte:window on:click={click} />
<header>
  <a href="/">Home</a>
  <a href="/posts">Posts</a>
  <a href="/profile">Profile</a>
</header>
<main class="page-container">
  {#if (params = $pattern("/posts/:id"))}
    <PostPage productId={params.id} />
  {:else if (params = $pattern("/"))}
    <HomePage />
  {:else if (params = $pattern("/posts"))}
    <PostsPage page={$query.page} search={$query.q} />
  {:else if (params = $pattern("/profile"))}
    <ProfilePage />
  {:else}
    <div>not found {$path}</div>
  {/if}
</main>

<style>
</style>
