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
_Relevant links such s Tiptap's documentation page, etc_

## Requirements

There are multiple methods to install Tiptap, each tailored to a specific use case. Detailed integration guides for different project types can be accessed [here](https://tiptap.dev/docs/editor/installation). In this article, we'll focus on creating a React project integrated with Tiptap, so you'll need Node.js and npm; if you don't have them installed, follow [this guide](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) to install them.

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

By default, Tiptap doesn't support inputting or outputting Markdown files.[^4] However, there is a community-developed npm package called `tiptap-markdown` that extends Tiptap to enable this. We'll go through the installation of this package and the creation of a simple editor that uses it.

**1. Install `tiptap-markdown`:**
We'll continue with the React project we created above. Install the `tiptap-markdown` package using npm:
```
npm install tiptap-markdown
```

**2. Import the package:**
Make a copy of App.js called Markdown.js. Add this import to the top of the file:
```
import { Markdown } from 'tiptap-markdown';
```

**3. Edit the editor:**
Add `Markdown` to the list of extensions used by the Tiptap editor. Since the file format has changed from HTML to Markdown, we'll change the initial content as well:
```
function MyEditor() {
  const editor = useEditor({
    extensions: [StarterKit, Markdown],
    content: '# Hello, TipTap!\nHello world!',
  });
}
```

**4. Render the new editor:**
Remove the definition of the `function App()` from the bottom of Markdown.js. Also change the line `export default App;` to `export default MyEditor;`.

Now, at the top of App.js, import the new Markdown editor from Markdown.js:
```
import MarkdownEditor from './Markdown';
```

Finally, render the new Markdown editor below the existing editor in App.js:
```
function App() {
  return (
    <div className="App">
      <h1>My TipTap Editor</h1>
      <MyEditor />
      <h1>My Markdown Editor</h1>
      <MarkdownEditor />
    </div>
  );
}
```

## Example with (something else Maybe)
_Maybe Ricky will work on this_

_Include gifs, code snippets, explainations_

## Citations

[^1]: https://tiptap.dev/blog/insights/tiptap-seriesseed
[^2]: https://tiptap.dev/product/editor
[^3]: https://tiptap.dev/docs/editor/introduction
[^4]: https://tiptap.dev/docs/editor/guide/output#not-an-option-markdown