<script lang="ts">
  import Editor from '$lib/components/Editor.svelte';

  let editorInstance: any; // Reference to the editor component

  // Example initial data (you'll likely fetch this from a database)
  const initialContent = {
    blocks: [
      {
        type: 'header',
        data: {
          text: 'Welcome to My Notion Clone',
          level: 1,
        },
      },
      {
        type: 'paragraph',
        data: {
          text: 'Start typing here...',
        },
      },
    ],
  };

  async function handleSave() {
    const savedData = await editorInstance.getEditorData();
    console.log('Saving data:', savedData);
    // Here you would send the data to your backend to be saved
  }
</script>

<h1>My Notion Clone</h1>

<Editor bind:this={editorInstance} initialData={initialContent} />

<button on:click={handleSave}>Save</button>
