> Heads up: This is meant to be a temporary repository, and will be archived if/once the PR is merged with the main repo by @azzlack, to fix the UI in accordance with the latest Sanity changes. Everything below is only changed enough to get this version working for you.

# Sanity Tabs Plugin

Input component for rendering fieldsets as tabs

[![NPM version](https://img.shields.io/npm/v/sanity-plugin-tabs-neue?style=for-the-badge)](https://www.npmjs.com/package/sanity-plugin-tabs-neue) [![NPM Downloads](https://img.shields.io/npm/dw/sanity-plugin-tabs-neue?style=for-the-badge)](https://www.npmjs.com/package/sanity-plugin-tabs-neue)

### How does it look?

![Preview](/images/previews.png?raw=true "Preview")

### Demo
Clone the originl [demo repository](https://github.com/azzlack/sanity-plugin-tabs-demo) and run `sanity start` to see how it works. This version is supposed to just be temporary, to work with the updated Sanity styling.

### How do I use it?

Just add `inputComponent: Tabs` to your field. Please note that the field type must be `object`.

```
import Tabs from "sanity-plugin-tabs-neue"

export default {
  type: "document",
  title: `Frontpage`,
  name: `frontpage`,
  fields: [
    {
      name: "content",
      type: "object",
      inputComponent: Tabs,

      fieldsets: [
        { name: "main", title: "Main", options: { sortOrder: 10 } },
        { name: "aside", title: "Aside", options: { sortOrder: 20 } },
        { name: "meta", title: "Meta", options: { sortOrder: 30 } },
      ],
      options: {
        // setting layout to object will group the tab content in an object fieldset border.
        // ... Useful for when your tab is in between other fields inside a document.
        layout: "object"
      },

      fields: [
        {
          type: "object",
          name: "mainTitle",
          title: "Main Title",
          fieldset: "main",

          fieldsets: [
            { name: "ingress", title: "Ingress" },
          ],

          fields: [
            {
              type: "string",
              name: "header",
              title: "Header"
            },
            {
              type: "string",
              name: "ingressText",
              title: "Text",
              fieldset: "ingress"
            },
          ]
        },
        {
          type: "string",
          name: "info",
          title: "Information",
          fieldset: "aside"
        },
        {
          type: "object",
          name: "aside",
          fieldset: "meta",
          inputComponent: Tabs,

          fieldsets: [
            { name: "tags", title: "Tags" },
            { name: "categories", title: "Categories" },
          ],

          fields: [
            {
              type: "string",
              name: "contentType",
              title: "Content Type",
              fieldset: "tags"
            },
            {
              type: "string",
              name: "category",
              title: "Category",
              fieldset: "categories"
            },
          ]
        },
      ]
    }
  ]
};
```

## Development
Run the following commands at the root of this repository.

```
npm i
npm link
```

Now you can start developing the plugin.  
To include it in your Sanity test site, navigate to the root folder of your cms project and run `npm link sanity-plugin-tabs`. You will now reference the local version of the when using `import Tabs from "sanity-plugin-tabs"` in your files.  

To debug the plugin files in you then need to run `sanity start --preserve-symlinks` in your cms project, and `npm run dev` in your sanity-plugin-tabs repository folder.