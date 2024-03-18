# A Guide on using Tiptap in a React CRUD app.

## What Is Tiptap

Tiptap, one of the leading open-source dev tools for rich content editors is trusted by many companies like Substack, AxiosHQ, and GitLab.[^1]

They have accumulated over 2 million downloads[^1] with their cool products such as Tiptap Content AI and Tiptap Collobatoration. 


![image](https://github.com/AshkanAleshams/learning-software-engineering.github.io/assets/90326959/a032584f-7d0b-4232-9d76-ee965e972f2b)[^2]


However for this guide, we will focus on the Tiptap Editor.

Tiptap Editor is a headless toolkit for building rich text WYSIWYG editors for Vue.js and React.js applications. Giving the user the complete freedom to fashion their own editor interface using customizable building blocks. 
It offers sensible defaults, an extensive array of extensions, and an intuitive API for tailoring every facet to the user's preferences.



## Why Use Tiptap

If you are looking for a powerful text editor for web applications, Tiptap is a great option to consider. Being open-source and built on the well-regarded ProseMirror library,[^3] Tiptap offers a solid foundation. It features real-time collaboration and boasts a rich library of [community extensions](https://github.com/ueberdosis/awesome-tiptap#community-extensions) that includes an extension that enables Markdown support. Starting with Tiptap is easy thanks to its free tier, but for those needing advanced features like AI integration and document commenting, [paid plans](https://tiptap.dev/pricing) are available, making Tiptap a versatile solution for diverse project needs.

## Relevant Links
For comprehensive resources related to Tiptap Editor, consider the following links:

- **Tiptap Official Website**: Detailed information on features and how to get started with Tiptap. [Visit Tiptap](https://tiptap.dev)

- **Documentation and Examples**: Access to extensive documentation and practical examples for using Tiptap. [Explore the docs](https://tiptap.dev/docs) and [View examples](https://tiptap.dev/examples)

- **GitHub Repository**: The source code and contribution guidelines are available on GitHub. [Check out the repository](https://github.com/ueberdosis/tiptap)

- **Guide and Tutorials on GitHub**: A detailed guide offering insights into configuring the editor, working with extensions, and more. [Read the guide](https://github.com/ueberdosis/tiptap/blob/main/docs/guide.md)

- **Community Discussions**: Engage with the Tiptap community on GitHub for help and discussions. [Join the conversation](https://github.com/ueberdosis/tiptap/discussions)


## Requirements

There are multiple methods to install Tiptap, each tailored to a specific use case. Detailed integration guides for different project types can be accessed [here](https://tiptap.dev/docs/editor/installation). In this article, we'll focus on creating a React project integrated with Tiptap, so you'll need Node.js and npm; if you don't have them installed, follow [this guide](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) to install them.

## Intro to Tiptap in React

_Include gifs, code snippets, explainations_

**1. Create a React Project:** 

You may use any other method of creating a React app if you wish.
``` 
npx create-react-app my-tiptap-project --template tiptap
cd my-tiptap-project
```

**2. Install TipTap:**

Install TipTap and its dependencies using npm or yarn:
```
npm install @tiptap/react @tiptap/pm @tiptap/starter-kit
```

**3. Import Tiptap components:**

Go to App.js and import the following:
```
import { Editor, EditorContent, EditorMenuBar } from '@tiptap/react';
import { useEditor } from '@tiptap/react/hooks';
import { EditorState } from '@tiptap/core';
import StarterKit from '@tiptap/starter-kit';
```

**4. Create a TipTap Editor Component:**

Create a new React component that will serve as your TipTap editor:
```
function MyEditor() {
  const editor = useEditor({
    extensions: [StarterKit],
    content: '<p>Hello, TipTap!</p>',
  });

  return (
    <div>
      <EditorMenuBar editor={editor} />
      <EditorContent editor={editor} />
    </div>
  );
}
```

**5. Render the Editor Component:**

Render your TipTap editor component within your main application component or any other desired location:
```
function App() {
  return (
    <div className="App">
      <h1>My TipTap Editor</h1>
      <MyEditor />
    </div>
  );
}

export default App;
```

**6. Run Your React Application:**

Start your React application to see TipTap in action:
```
npm start
```

## Example with Markdown Editor in React
_Include gifs, code snippets, explainations_


## Using Tiptap with Markdown Extension

To use Tiptap editor with the Markdown extension, follow these steps:

1. **Initialize the Tiptap editor with the Markdown extension:**

   ```javascript
   export default function Tiptap() {
     return (
       <EditorProvider
         slotBefore={<MenuBar />}
         extensions={extensions}
         content={content}
         onUpdate={({ editor }) => {
           const new_markdown = editor.storage.markdown.getMarkdown();
           console.log(new_markdown);
         }}
       ></EditorProvider>
     );
   }


2. **Retrieve Markdown content:**

   Within the `onUpdate` function, use the `getMarkdown()` method on the editor object to retrieve the Markdown representation of the content.
   
   ```javascript
   const new_markdown = editor.storage.markdown.getMarkdown();
3. **Initialize the Tiptap editor without the Markdown extension**

   ```javascript
   export default function Tiptap() {
   return (
    <EditorProvider
      slotBefore={<MenuBar />}
      extensions={extensions}
      content={content}
      onUpdate={({ editor }) => {
        const json = editor.getJSON();
        const html = editor.getHTML();
        console.log(json);
        console.log(html);
      }}
    ></EditorProvider>
   );}


## Citations

[^1]: https://tiptap.dev/blog/insights/tiptap-seriesseed
[^2]: https://tiptap.dev/product/editor
[^3]: https://tiptap.dev/docs/editor/introduction
