---
title: "CSS Counters"
seoTitle: "CSS Counters"
seoDescription: "CSS Counters make style easy and better if used efficiently. so here is a guide to it."
datePublished: Tue Jun 06 2023 05:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clijtboqw0oy8amnvfnnj11yg
slug: css-counters
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685816189901/729e77fc-ae7c-4e2c-b68a-a576a1459feb.png
tags: css, web-development, styleguide, webdev

---

CSS Counters are an incredibly useful feature that allows web developers to create custom numbering systems and enhance the styling of lists and headings. In this blog post, we will dive into CSS counters, explore their capabilities, and provide practical examples along with their outputs to help you grasp the concept and leverage it effectively in your web projects.

Understanding CSS Counters: CSS counters are variables that can be incremented or decremented to create a numbering system for HTML elements. They can be used to automatically generate numbers or labels for ordered lists, unordered lists, and headings. CSS counters rely on two main properties:

1. `counter-reset`: This property initializes or resets the value of a counter. By default, the counter's value is set to zero.
    
2. `counter-increment`: This property increments or decrements the value of a counter.
    

Example 1: Creating Numbered Lists Let's start with a simple example to create a custom numbered list using CSS counters:

```xml
<style>
  ol {
    counter-reset: my-counter;
    list-style-type: none;
  }

  li::before {
    counter-increment: my-counter;
    content: counter(my-counter) ". ";
  }
</style>

<ol>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ol>
```

Output:

1. First item
    
2. Second item
    
3. Third item
    

In this example, we first set the counter `my-counter` to zero using `counter-reset` for the `ol` (ordered list) element. We then utilize the `::before` pseudo-element to display the counter value before each list item. The `content` property uses the `counter()` function to retrieve and display the value of `my-counter` followed by a dot and a space.

Example 2: Nesting Counters CSS counters can be nested, allowing for more complex numbering systems. Let's create a nested list with custom numbering:

```xml
<style>
  ol {
    counter-reset: chapter;
    list-style-type: none;
  }

  li::before {
    counter-increment: chapter;
    content: "Chapter " counter(chapter) ". ";

    ol {
      counter-reset: section;
      list-style-type: none;
    }

    li::before {
      counter-increment: section;
      content: counter(chapter) "." counter(section) " ";
    }
  }
</style>

<ol>
  <li>Introduction
    <ol>
      <li>Overview</li>
      <li>Goals</li>
    </ol>
  </li>
  <li>Main Content
    <ol>
      <li>Section 1</li>
      <li>Section 2</li>
    </ol>
  </li>
</ol>
```

Output:

1. Introduction
    
    1.1. Overview
    
    1.2. Goals
    
2. Main Content
    
    2.1. Section 1
    
    2.2Section 2
    

Explanation: In this example, we define a counter called `chapter` and increment it for each top-level list item using `counter-increment`. We display the counter value preceded by the text "Chapter" and followed by a dot and a space. Inside each top-level list item, we reset a nested counter called `section` using `counter-reset` and increment it for each nested list item. The nested list items display the combined values of `chapter` and `section` with appropriate numbering.

Example 3: Customizing Heading Styles CSS counters can be applied to headings to create custom numbering styles. Let's see how to achieve this:

```xml
<style>
  body {
    counter-reset: heading;
  }

  h2::before {
    counter-increment: heading;
    content: counter(heading) ". ";
  }
</style>

<h2>Title 1</h2>
<p>Content for title 1.</p>

<h2>Title 2</h2>
<p>Content for title 2.</p>

<h2>Title 3</h2>
<p>Content for title 3.</p>
```

Output:

1. Title 1 Content for title 1.
    
2. Title 2 Content for title 2.
    
3. Title 3 Content for title 3.
    

In this example, we set the counter `heading` to zero using `counter-reset` for the `body` element. We then increment the counter by one for each `h2` heading using `counter-increment`. The `::before` pseudo-element is used to display the counter value followed by a dot and a space before each heading.

CSS counters offer a flexible way to create custom numbering systems and enhance the styling of lists and headings. By understanding the `counter-reset` and `counter-increment` properties, you can effectively utilize CSS counters in your web development projects. The examples provided in this blog post demonstrate different use cases along with their corresponding outputs and explanations. Incorporate CSS counters into your styling arsenal to elevate the visual appeal and structure of your web content. Happy coding!

**If you find value in this content, don't forget to like and comment on the blog post. Feel free to follow me on** [**Twitter**](https://twitter.com/dhanuks26)**,** [**GitHub**](https://github.com/DhanushGowda26)**, and** [**Hashnode**](https://dhanushks.hashnode.dev/) **for more valuable content. Stay tuned for future articles where we explore more such content.**

**Thank you for reading! 🙏 Your time and attention are greatly appreciated! If you have any further questions or need additional information, please don't hesitate to ask. 😊**