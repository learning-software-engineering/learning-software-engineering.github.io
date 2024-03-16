# A Guide on using Tiptap in a React CRUD app.

## What Is Tiptap

Tiptap, one of the leading open-source dev tools for rich content editors is trusted by many companies like Substack, AxiosHQ, and GitLab.

They have accumulated over 2 million downloads with their cool products such as Tiptap Content AI and Tiptap Collobatoration. 


![image](https://github.com/AshkanAleshams/learning-software-engineering.github.io/assets/90326959/a032584f-7d0b-4232-9d76-ee965e972f2b)


However for this guide, we will focus on the Tiptap Editor.

Tiptap Editor is a headless toolkit for building rich text WYSIWYG editors for Vue.js and React.js applications. Giving the user the complete freedom to fashion their own editor interface using customizable building blocks. 
It offers sensible defaults, an extensive array of extensions, and an intuitive API for tailoring every facet to the user's preferences.



## Why Use Tiptap

If you are looking for a powerful text editor for web applications, Tiptap is a great option to consider. Being open-source and built on the well-regarded ProseMirror library,[^1] Tiptap offers a solid foundation. It features real-time collaboration and boasts a rich library of community extensions[^2] that includes an extension that enables Markdown support. Starting with Tiptap is easy thanks to its free tier, but for those needing advanced features like AI integration and document commenting, paid plans[^3] are available, making Tiptap a versatile solution for diverse project needs.

## Relevant Links
_Relevant links such s Tiptap's documentation page, etc_

## Requirements
_React, npm, etc installation stuff_

## Intro to Tiptap in React

_Include gifs, code snippets, explainations_

**1. Create a React Project:**
You may use any other method of creating a React app if you wish.
``` 
npx create-react-app my-tiptap-project
cd my-tiptap-project
```

**2. Install TipTap:**
Install TipTap and its dependencies using npm or yarn:
```
npm install tiptap @tiptap/react
```

**3. Import Tiptap components:**
If you havent, create a new file called App.js and import the following:
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

## Example with Markdown Editor in React
_Include gifs, code snippets, explainations_


## Example with (something else Maybe)
_Maybe Ricky will work on this_

_Include gifs, code snippets, explainations_

## Citations
_Include formal citation_
[^1]: https://tiptap.dev/docs/editor/introduction
[^2]: https://github.com/ueberdosis/awesome-tiptap#community-extensions
[^3]: https://tiptap.dev/pricing
