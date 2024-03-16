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
_Relevant links such s Tiptap's documentation page, etc_

## Requirements

There are multiple methods to install Tiptap, each tailored to a specific use case. Detailed integration guides for different project types can be accessed [here](https://tiptap.dev/docs/editor/installation). In this article, we'll focus on creating a React project integrated with Tiptap, so you'll need Node.js and npm; if you don't have them installed, follow [this guide](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) to install them.

## Intro to Tiptap in React

_Include gifs, code snippets, explainations_

**1. Create a Project** 

You may use any other method of creating a React app if you wish, but 
[Tiptap Create React App template by @alb](https://github.com/alb/cra-template-tiptap) is the quickest way. 

``` 
npx create-react-app my-tiptap-project --template tiptap

```

This will also install the dependencies for you!


**2. Run the Project**

Start your React application to see TipTap in action.
```
cd my-tiptap-project

npm start
```

**3. Add a Menu Bar:**

Improve your editor by adding a menu bar to Tiptap.jsx.


```
import './Tiptap.css'

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

**4. Make it Look Better**

Create a style sheet and name it Tiptap.css

```
/* Basic editor styles */
.tiptap {
    > * + * {
      margin-top: 0.75em;
    }

    h1,
    h2,
    h3 {
      line-height: 1.1;
    }
  
    code {
      background-color: rgba(#616161, 0.1);
      color: #616161;
    }
  
    pre {
      background: #0D0D0D;
      color: #FFF;
      font-family: 'JetBrainsMono', monospace;
      padding: 0.75rem 1rem;
      border-radius: 0.5rem;
  
      code {
        color: inherit;
        padding: 0;
        background: none;
        font-size: 0.8rem;
      }
    }
  
  }

```

**5. Install new Dependencies**

Install tiptap/extension-color and tiptap/extension-text-style packages.
```
npm install @tiptap/extension-color @tiptap/extension-text-style
```

**6. Enjoy Your New Editor**
```
npm start
```


## Example with Markdown Editor in React
_Include gifs, code snippets, explainations_


## Example with (something else Maybe)
_Maybe Ricky will work on this_

_Include gifs, code snippets, explainations_

## Citations

[^1]: https://tiptap.dev/blog/insights/tiptap-seriesseed
[^2]: https://tiptap.dev/product/editor
[^3]: https://tiptap.dev/docs/editor/introduction
