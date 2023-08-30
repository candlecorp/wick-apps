<script lang="ts">
  import { Input, Label, Textarea, Card } from "flowbite-svelte";
  import { type BlogObject, type BlogTitlesObject } from "./lib/types";
  import { onMount } from "svelte";

  let posts: BlogTitlesObject[] = [];
  let selectedPost: BlogObject | null = null;
  let newTitle = "";
  let newContent = "";

  onMount(() => {
    fetch("/blogs")
      .then((response) => response.json())
      .then((data) => {
        posts = data.blogs.map(
          (blog: { value: BlogTitlesObject }) => blog.value
        );
      })
      .catch((error) => console.error("Error fetching blogs:", error));
  });

  let getPost = (id: number) => {
    fetch(`/blogs/get/${id}`)
      .then((response) => response.json())
      .then((data) => {
        selectedPost = data.blog;
      })
      .catch((error) => console.error("Error fetching blog post:", error));
  };

  let createPost = async () => {
    const payload = {
      title: newTitle,
      content: newContent,
    };

    try {
      const response = await fetch("/blogs/create", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(payload),
      });

      if (response.ok) {
        newTitle = "";
        newContent = "";
        fetch("/blogs")
          .then((response) => response.json())
          .then((data) => {
            posts = data.blogs.map(
              (blog: { value: BlogTitlesObject }) => blog.value
            );
          })
          .catch((error) => console.error("Error fetching blogs:", error));
      } else {
        console.error("Failed to create post:", await response.text());
      }
    } catch (error) {
      console.error("Error creating post:", error);
    }
  };
</script>

<main class="container mx-auto mt-10">
  <div class="text-center mb-10">
    <h1 class="text-4xl font-bold">Blog</h1>
  </div>
  <div class="mx-auto mt-10 w-[300px]">
    <form class="space-y-4" on:submit|preventDefault={createPost}>
      <div>
        <label for="title" class="block text-sm font-medium text-gray-600"
          >Title</label
        >
        <input
          type="text"
          id="title"
          name="title"
          class="mt-1 p-2 w-full border rounded-md"
          bind:value={newTitle}
        />
      </div>
      <div>
        <label for="content" class="block text-sm font-medium text-gray-600"
          >Content</label
        >
        <textarea
          id="content"
          name="content"
          class="mt-1 p-2 w-full h-32 border rounded-md"
          bind:value={newContent}
        />
      </div>
      <div>
        <button
          type="submit"
          class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
          >Submit</button
        >
      </div>
    </form>
  </div>

  <div class="flex mt-10">
    <div class="w-[200px] p-4 border-r">
      <h2 class="text-2xl mb-4">Posts</h2>
      <ul>
        {#if posts.length === 0}
          <li>No posts</li>
        {:else}
          {#each posts as post}
            <li class="mb-2">
              <a
                class="text-blue-500 hover:underline cursor-pointer"
                on:click={() => getPost(post.id)}>{post.title}</a
              >
            </li>
          {/each}
        {/if}
      </ul>
    </div>

    <div class="w-[400px] p-4">
      {#if selectedPost}
        <div class="border p-4 rounded">
          <h3 class="text-3xl mb-4">{selectedPost.title}</h3>
          <p class="text-lg">{selectedPost.content}</p>
        </div>
      {:else}
        <p>Select a post to view its content.</p>
      {/if}
    </div>
  </div>
</main>
