# A Guide on using Tiptap in a React CRUD app.

## What Is Tiptap

Tiptap, one of the leading open-source dev tools for rich content editors is trusted by many companies like Substack, AxiosHQ, and GitLab.[^1]

They have accumulated over 2 million downloads[^1] with their cool products such as Tiptap Content AI and Tiptap Collobatoration. 


![Untitled design (4)](https://github.com/AshkanAleshams/learning-software-engineering.github.io/assets/90326959/f56018c2-e7ef-478f-95d2-de19838cc1c7)


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

**1. Create a project** 

You may use any other method of creating a React app if you wish, but 
[Tiptap Create React App template by @alb](https://github.com/alb/cra-template-tiptap) is the quickest way. 

``` 
npx create-react-app my-tiptap-project --template tiptap

```

This will also install the dependencies for you!


**2. Run the project**

Start your React application to see Tiptap in action.
```
cd my-tiptap-project

npm start
```

**3. Add a menu bar**

Improve your editor by adding a menu bar to Tiptap.jsx.

Each button in the menu bar example code below takes three arguments. Taking the bold button as an example:
- The [`onClick`](https://react.dev/learn/responding-to-events#adding-event-handlers) function makes the editor toggle any selected text between bolded and non-bolded modes.
- The [`disabled`](https://www.w3schools.com/tags/att_button_disabled.asp) argument determines whether the bold button should be faded out because the selected text cannot be bolded.
- The [`className`](https://legacy.reactjs.org/docs/faq-styling.html) is `is-active` or blank depending on whether the selected text is bolded. If the `is-active` `className` is present, the bold button in the menu bar will be emphasized.

Here is the code sourced from [here](https://tiptap.dev/docs/editor/installation/react):
<details>
  <summary>Tiptap.jsx</summary>
  
  ```
  import { Color } from '@tiptap/extension-color'
  import ListItem from '@tiptap/extension-list-item'
  import TextStyle from '@tiptap/extension-text-style'
  import { EditorProvider, useCurrentEditor } from '@tiptap/react'
  import StarterKit from '@tiptap/starter-kit'
  import React from 'react'
  
  const MenuBar = () => {
    const { editor } = useCurrentEditor()
  
    if (!editor) {
      return null
    }
  
    return (
      <>
        <button
          onClick={() => editor.chain().focus().toggleBold().run()}
          disabled={
            !editor.can()
              .chain()
              .focus()
              .toggleBold()
              .run()
          }
          className={editor.isActive('bold') ? 'is-active' : ''}
        >
          bold
        </button>
        <button
          onClick={() => editor.chain().focus().toggleItalic().run()}
          disabled={
            !editor.can()
              .chain()
              .focus()
              .toggleItalic()
              .run()
          }
          className={editor.isActive('italic') ? 'is-active' : ''}
        >
          italic
        </button>
        <button
          onClick={() => editor.chain().focus().toggleStrike().run()}
          disabled={
            !editor.can()
              .chain()
              .focus()
              .toggleStrike()
              .run()
          }
          className={editor.isActive('strike') ? 'is-active' : ''}
        >
          strike
        </button>
        <button
          onClick={() => editor.chain().focus().toggleHeading({ level: 1 }).run()}
          className={editor.isActive('heading', { level: 1 }) ? 'is-active' : ''}
        >
          h1
        </button>
        <button
          onClick={() => editor.chain().focus().toggleHeading({ level: 2 }).run()}
          className={editor.isActive('heading', { level: 2 }) ? 'is-active' : ''}
        >
          h2
        </button>
        <button
          onClick={() => editor.chain().focus().toggleHeading({ level: 3 }).run()}
          className={editor.isActive('heading', { level: 3 }) ? 'is-active' : ''}
        >
          h3
        </button>
        <button
          onClick={() => editor.chain().focus().toggleCodeBlock().run()}
          className={editor.isActive('codeBlock') ? 'is-active' : ''}
        >
          code block
        </button>
        <button
          onClick={() => editor.chain().focus().undo().run()}
          disabled={
            !editor.can()
              .chain()
              .focus()
              .undo()
              .run()
          }
        >
          undo
        </button>
        <button
          onClick={() => editor.chain().focus().redo().run()}
          disabled={
            !editor.can()
              .chain()
              .focus()
              .redo()
              .run()
          }
        >
          redo
        </button>
        <button
          onClick={() => editor.chain().focus().setColor('#958DF1').run()}
          className={editor.isActive('textStyle', { color: '#958DF1' }) ? 'is-active' : ''}
        >
          purple
        </button>
      </>
    )
  }
  
  const extensions = [
    Color.configure({ types: [TextStyle.name, ListItem.name] }),
    TextStyle.configure({ types: [ListItem.name] }),
    StarterKit.configure({
      bulletList: {
        keepMarks: true,
        keepAttributes: false, // TODO : Making this as `false` becase marks are not preserved when I try to preserve attrs, awaiting a bit of help
      },
      orderedList: {
        keepMarks: true,
        keepAttributes: false, // TODO : Making this as `false` becase marks are not preserved when I try to preserve attrs, awaiting a bit of help
      },
    }),
  ]
  
  const content = `
  <h2>
    Hi there,
  </h2>
  <p>
    Isn’t that great? And all of that is editable. But wait, there’s more. Let’s try a code block:
  </p>
  <pre><code class="language-css">body {
  display: none;
  }</code></pre>
  <p>
    I know, I know, this is impressive. It’s only the tip of the iceberg though. Give it a try and click a little bit around. Don’t forget to check the other examples too.
  </p>
  
  `
  
  export default function Tiptap () {
    return (
      <EditorProvider slotBefore={<MenuBar />} extensions={extensions} content={content}></EditorProvider>
    )
  }
  ```

</details>



**4. Install new dependencies**

Install tiptap/extension-color and tiptap/extension-text-style packages.
```
npm install @tiptap/extension-color @tiptap/extension-text-style
```

**5. Enjoy Your new editor**
```
npm start
```

**6. Use the output from the editor**

At the bottom of Tiptap.jsx, add an `onUpdate` prop to the EditorProvider, using the `getHTML()` and `getJSON()` method on the editor object to retrieve the HTML and JSON representations, respectively, of the content in the editor when the user changes it and print it to the browser's console.
  ```javascript
  export default function Tiptap () {
    return (
      <EditorProvider slotBefore={<MenuBar />} extensions={extensions} content={content} onUpdate={({ editor }) => {
        const json = editor.getJSON();
        const html = editor.getHTML();
        console.log(json);
        console.log(html);
      }}></EditorProvider>
    )
  }
  ```

## Example with Markdown Editor in React

By default, Tiptap doesn't support input from or output to Markdown files.[^4] However, there is a community-developed npm package called `tiptap-markdown` that extends Tiptap to enable this. We'll go through the installation of this package and the creation of a simple editor that uses it.

**1. Install `tiptap-markdown`**

We'll continue with the React project we created above. Install the [`tiptap-markdown`](https://www.npmjs.com/package/tiptap-markdown) package using npm:
```
npm install tiptap-markdown
```

**2. Import the package**

Make a copy of Tiptap.jsx called Markdown.jsx. Add this import to the top of the file:
```
import { Markdown } from 'tiptap-markdown';
```

**3. Edit the editor**

In Markdown.jsx, add `Markdown` to the list of extensions used by the Tiptap editor. Since the input file format has changed from HTML to Markdown, we'll change the initial content as well:
````
const extensions = [
  [...keep the existing extensions...]
  Markdown,
]

const content = `
## Hi again,
Here is a Markdown version!
\`\`\`css
body {
display: none;
}
\`\`\`
`
````

**4. Render the new editor**

At the top of App.js, import the new Markdown editor from Markdown.jsx:
```
import Markdown from './Markdown';
```

Finally, render the new Markdown editor below the existing editor in App.js:
```
const App = () => {
  return (
    <div className="App">
      <Tiptap />
      <Markdown />
    </div>
  );
};
```

**5. See both editors in action**
```
npm start
```

**6. Use the output from the Markdown editor**

At the bottom of Markdown.jsx, add an `onUpdate` prop to the EditorProvider, using the `getMarkdown()` method on the editor object to retrieve the Markdown representation of the content in the editor when the user changes it and print it to the browser's console.
  ```javascript
  export default function Tiptap () {
    return (
      <EditorProvider slotBefore={<MenuBar />} extensions={extensions} content={content} onUpdate={({ editor }) => {
         const new_markdown = editor.storage.markdown.getMarkdown();
         console.log(new_markdown);
      }}></EditorProvider>
    )
  }
  ```

![Untitled design (5)](https://github.com/AshkanAleshams/learning-software-engineering.github.io/assets/90326959/51e0072e-776b-41bb-9360-4307c56e45c5)


## Citations

https://tiptap.dev/blog/insights/tiptap-seriesseed

https://tiptap.dev/product/editor

https://tiptap.dev/docs/editor/introduction

https://tiptap.dev/docs/editor/installation/react

https://github.com/alb/cra-template-tiptap

https://tiptap.dev/product/editor

https://tiptap.dev/docs/editor/guide/output

[^1]: [Tiptap Seriesseed - Insights](https://tiptap.dev/blog/insights/tiptap-seriesseed)
[^2]: [Tiptap Editor - Product](https://tiptap.dev/product/editor)
[^3]: [Tiptap Editor - Introduction](https://tiptap.dev/docs/editor/introduction)
[^4]: [Tiptap Editor - Output](https://tiptap.dev/docs/editor/guide/output)
