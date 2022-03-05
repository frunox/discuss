%{
title: "Building the Blog - Parsing Markdown",
author: "lonesome-coder",
tags: ~w(firebase firestore cloud storage),
description: "Processing markdown files and rendering HTML to the browser is straightforward with NimblePublisher.",
}

---

![javascript code]()

In an earlier [post](http://localhost:3000/post/acq-markdown-not-a-sales-pitch), I discussed why I use Markdown to create the posts. Now I'll show how to read in the post files, including metadata, and use some tools to parse the metadata and render the content to the browser.

(NOTE: This post has been [updated](https://acodersquest.com/post/acq-building-the-blog-more-on-markdown) to show an improved method of processing the Markdown files. The concepts shown below are still used.)

## Loading a Markdown File in React

First, add `<input type='file' onChange={metadataFileSelectedHandler} />` in the JSX to render a file picker.

React prevents the use the Nodejs filesystem. But, you can read files using the JavaScript [FileReader](https://www.w3docs.com/learn-javascript/file-and-filereader.html) class. I use hooks and functional components, so this is the setup:

```elixir
function Admin() {
  const [mData, setMData] = useState('')
  }
```

The variable `rawFile` stores the selected file. A new `reader` object is created, and the `FileReader` method `readAsText()` reads in the file as a string. The `onload` method calls `reader.result` which loads the string into `file`, which is copied into the state variable `markdownFile`. This holds the entire \*.md file, including the metadata.

## Parsing the Metadata

Separating the metadata from the markdown file is simple. I created a button in the JSX that triggers `parseHandler`:

## Storing the Posts

The metadata is assigned to `postObject`, and the content is added as another field. All the data is in string format.

Now the `postUid` in the metadata comes into play. By default, Firestore assigns a random `uid` to each document (or record). It allows you to create your own `uid`, however, as long as it is unique. Using a custom `uid` makes it easier to identify each post in the Firestore dashboard, and, more importantly, allows Firebase update existing posts.

## Retrieving the Posts

This is done in the _App_ component using _useEffect()_ to limit the number of calls to Firestore.

> _“One child, one teacher, one book, one pen can change the world.”_
>
> Malala Yousafzai

## How to Render Markdown in React

Now, the posts are stored and ready to be to shown to the world. But, it's all just strings at this point. How is it rendered by React?
