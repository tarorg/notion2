<script lang="ts">
    import { onMount } from 'svelte';
    import type { API, EditorConfig } from '@editorjs/editorjs';
  
    export let initialData: any = undefined;
    export let readOnly: boolean = false;
  
    let editor: any;
    let editorContainer: HTMLDivElement;
  
    export async function getEditorData() {
      if (editor) {
        return await editor.save();
      }
      return null;
    }
  
    onMount(async () => {
      // Dynamically import EditorJS and all tools
      const EditorJS = (await import('@editorjs/editorjs')).default;
      const Header = (await import('@editorjs/header')).default;
      const List = (await import('@editorjs/list')).default;
      const Paragraph = (await import('@editorjs/paragraph')).default;
      const ImageTool = (await import('@editorjs/image')).default;
    const Checklist = (await import('@editorjs/checklist')).default;
    const Table = (await import('@editorjs/table')).default;
    const CodeTool = (await import('@editorjs/code')).default;
    const RawTool = (await import('@editorjs/raw')).default;
    const Embed = (await import('@editorjs/embed')).default;
    const Quote = (await import('@editorjs/quote')).default;
    const Delimiter = (await import('@editorjs/delimiter')).default;
    const Marker = (await import('@editorjs/marker')).default;
    const InlineCode = (await import('@editorjs/inline-code')).default;
  
      const config: EditorConfig = {
        holder: editorContainer,
        readOnly: readOnly,
        tools: {
        header: {
          class: Header,
          inlineToolbar: ['marker', 'inlineCode'],
          },
        list: {
          class: List,
          inlineToolbar: true,
              },
        paragraph: {
          class: Paragraph,
          inlineToolbar: true,
            },
        image: {
          class: ImageTool,
          config: {
            endpoints: {
              byFile: '/api/uploadImage',
              byUrl: '/api/fetchUrl',
        },
        },
        },
        checklist: {
          class: Checklist,
          inlineToolbar: true,
        },
        table: {
          class: Table,
          inlineToolbar: true,
        },
        code: CodeTool,
        raw: RawTool,
        embed: {
          class: Embed,
          config: {
            services: {
              youtube: true,
              codepen: true,
              // Add other embed services you want
            },
          },
        },
        quote: {
          class: Quote,
          inlineToolbar: true,
        },
        delimiter: Delimiter,
        marker: Marker,
        inlineCode: InlineCode,
      },
      data: initialData,
      onChange: (api: API) => {
        console.log("Now I know that Editor's content changed!");
      },
    };

    editor = new EditorJS(config);
  });
  </script>
  
  <div bind:this={editorContainer} id="editorjs"></div>
  
  <style>
  /* Add some basic styling (customize as needed) */
    #editorjs {
      border: 1px solid #ccc;
      border-radius: 4px;
    }
  </style>