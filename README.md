# Webkit Alpha

This repository is for new Webkit development updates.

## Update 0.1

This version of the Webkit features:

- A new parser for generating sites using XML syntax and Markdown for shorter and simpler configurations. An example of this syntax can be seen in use [here](https://edgeryders.eu/raw/13810.json).
- A sandbox and local mode for switching between loading local and remote configurations
- A template system for loading specific layouts from a configuration 
- A theme system for loading custom styles from a configuration
- Improved inline styling options 

## XML Parser

The XML parser will not replace the JSON configuration syntax, but provide an easier option for project managers to generate a site from scratch.

### The template syntax includes a front matter in YAML for configuring the site

```
site:
  title: Site Title
  template: Template Name (Vue template, optional)
  theme: Edgeryders (CSS theme, optional)
  lang: en-US (Language, optional)

```

Depending on the template loaded, additional template variables can be set in the frontmatter.

### For the Campaign template, the following variables can be set

```
<Config>

menu: 
  anchor: true (displays anchor links to sections with an ID)
  links: (displays external links)
  	- text: link text 1
  	  url: https://...
  	- text: link text 2
  	  url: https://...
header:
  image: https://i.redd.it/x5zojh91awfz.jpg (header image)
  social: ['url', 'twitter', 'facebook', 'linkedin', 'email'] (social links to display)

</Config>

```

### A simple XML template

```
<Webkit>

<Config>

My YAML frontmatter inside a code block.

</Config>

<Header>

  <Text>
	  ## My header title.
	  My header paragraph text

	  [My header link #1](url)
	  [My header link #2](url)
  </Text>

</Header>

<Content>

  <Text> A text view with html, embedded images, embedded video </Text>
  <Text> 
     ### A subtitle
     Another text view
   </Text>
  
</Content>

</Webkit>
```

## Sandbox & Local Mode

You can set the Webkit to read from multiple configurations:
- Sandbox mode can load multiple configurations based on the URL of the site
- Local mode loads a single configuration file hosted on the server

### This mode is set in ```src/data/config.yaml```

```
---
baseUrl: https://edgeryders.eu
title: Webkit Sandbox
mode: local (or sandbox)
```

When in sandbox mode, you can provide a default topic ID to read the configuration from the root address.

To load another configuration topic, enter the topic ID after the trailing slash of the address where Webkit is deployed:

For example, to load the configuration of topic ```13810``` from the local server running webkit:

```
http://localhost:8080/13810
```

## Templates & Themes

There are cases where different sites need specific layouts and styling. The templates directory hosts Vue templates that can be loaded conditionnally based on the configuration.

Templates require development of a Vue component located in the ```src/components/templates``` directory, while Themes are CSS files that can be loaded locally or remotely. 

Local themes are located in the ```src/assets/themes``` directory.

The template and theme of a site are defined in the frontmatter of the configuration. If no template or theme is specified, Webkit will default to the standard configuration.

```
---
baseUrl: https://edgeryders.eu
title: Webkit Sandbox
mode: local (or sandbox)
template: Campaign
theme: edgeryders.scss (or topic ID with code block containing CSS)
```

### Inline styling

In the XML syntax, blocks can be styled with standard inline css.


#### An example of inline styling on Blocks and Views

```
<Content style="background: black; padding: 30px">

## My content title

<Text style="background: blue; font-family: Georgia, serif">
My text view with Georgia
</Text>

</Content>
```

Markdown elements can also be styled using Block Inline Attribute Lists, which can be used to attach attributes such as a class, id and style to Markdown text. 

#### An example of inline styling with Markdown

```
<Content>

## My red title{style="color: red"}

</Content>
```

## Installation for local development

### Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```
