---
layout: post
title:  Accessibility and HTML5
date:   2017-05-31 03:34:40 +0000
---

Before the addition of semantic tags in HTML5, `<div>` and `<span>` were used to style and section different areas of a webpage. This caused html docs to be filled with divs, aka divitis, which made it difficult for developers and browser to easily differentiate between different elements. The semantic tags added in HTML5 were created based on popular id and class attributes developers were using in their div and other elements (Fun Fact: [Google did a study of over a billion html documents to get this data](https://developers.google.com/webmasters/state-of-the-web/?csw=1)).  Besides providing meaningful structure to pages, HTML5 makes websites more accessible to those with disabilities. 
 
Assistive technology such as screen reader software and braille displays for those with impaired vision, or navigation via voice commands for those with mobility impairments. I am going to focus on screen readers for the purpose of this blog post because it is used most often by visually impaired individuals and benefits the most from HTML5 semantic tags. The use of semantic tags allows for the html document to be cleaner (less divs) which makes it easier for screen readers to interpret the data and present it to the user in a way that is useful. Screen readers work by providing the user with information about menus, headings, and other content on a website. The screen readers use landmarks to navigate the page, differentiating between different types of content on the page using the HTML5 semantic tags. `<header>`, `<footer>`, `<nav>`, `<aside>`, `<main>`, and `<section>` elements are all used as landmarks for screen readers. Users browse sites by hearing a list of the landmarks and decide where to navigate from there. However, these programs can only interpret what is given to them, so if your HTML document relies on too many divs for formatting and layout and does not include these landmark elements, it becomes difficult to differentiate between different sections of a webpage when using assistive technologies. 
 
Due to the use of assistive technologies (and for the sanity of developers who look at your code in the future), semantic tags should only be used when the content within the element has a meaning related to the tag. 

#### Here is a quick guide to the HTML5 semantic elements and their use.
 
**Article** - An article is a self-contained composition in a page that can be independently distributable. It should have a header element as a child of the article element.
```
<article>
    <h3>My Blog Post</h3>
    <p>This is an awesome blog post about awesome things!</p>
</article>
```
 
**Aside** - An aside contains content connected tangentially to the main content. 
```
<p>The painting of Adele Bloch-Bauer by Gustav Klimt was the center of a legal battle between the heirs of Adele Bloch-Bauer and the Austrian government. </p>
 
<aside>
    <h5>Gustav Klimt</h5>
    <p>(1862-1918) Klimt was an Austrian Art Nouveau painter. He is known for his painting “The Kiss”.</p>
</aside>
```
 
**Details and Summary** - The details element contains additional details that the user can view or hide. The summary gives a visible heading to the details element.
```
<details>
    <summary>Contact Us</summary>
    <p>555-1234</p>
    <p>email@email.com</p>
</details>
```
 
**Figure and Figcaption** - Defines an independent figure that has essential data to the page but could easily moved elsewhere. The figcaption element goes inside figure and is optional. This update in HTML5 makes an explicit association between images and captions, which is beneficial for those using assistive technology. 
```
<figure>
    <img src=”chart.jpg” alt=”My cats weight over time”>
    <figcaption>This chart shows how my cat’s weight has increased over time.</figcaption>
</figure>
```
 
**Footer** - The footer specifies the footer for nearest section or element, typically has author, copyright, and other information related to previous section. 
``` 
<footer>
    Copyright 2017 Leigh Passamano. All Rights Reserved.
</footer>
```
 
**Header** - The header groups introductory or navigational aids, several header elements can be included in one document. 
```
<article>
    <header>
        <h1>The History of Cats in Art</h1>
        <p>Cats have been appearing in art for as long as humans have been making art.</p>
    </header>
    <p>Dating back to cave paintings, cats have been the subject of some of the greatest works of art. </p>
</article>
```
 
**Main** - Defines the main content of the document. 
```
<main>
    <h1>Renaissance Art</h1>
    
    <article>
        <h2>Renaissance in Italy</h2>
        <p>Italian Renaissance art is characterized by a renewed interest in classical antiquity and more naturalistic depictions in painting and sculptures.</p>
    </article>
 
    <article>
        <h2>Renaissance in Northern Europe</h2>
        <p>The Italian Renaissance influenced the works of artists in Northern Europe, which evolved into unique characteristics of the different nationalities and regions.</p>
    </article>
 
</main>
```
 
**Mark** - Highlights or marks text, usually for reference. 
```
<p>There ain’t no party like a Liz Lemon party, cuz a Liz Lemon party is <mark>mandatory</mark>!</p>
```
 
**Nav** - Defines the set of navigation links.
```
<nav>
    <a href=”#”>Home</a>
    <a href=”#”>About</a>
    <a href=”#”>Contact</a>
</nav>
```
 
**Section** - The section element defines the different sections of a document, and should have a heading element as a child. 
```
<section>
    <h3>Recent Blog Posts</h3>
    <ul>
        <li>Why is the sky blue?</li>
        <li>Is my cat too fat?</li>
    </ul>
</section>
```
 
Time - Defines date/time information in a format that is readable to users and can include a datetime attribute that provides the date/time in a machine readable format. The time tag is what allows you to add events to your calendar from a page! 
```
<p>Our next meetup will be on <time datetime=””2017-09-12 18:00”>September 12 at 6pm</time> at the NYC Flatiron campus.</p>
```
 
And if you are confused about when you should use semantic elements, here is a [handy PDF flowchart to help you out.](http://html5doctor.com/downloads/h5d-sectioning-flowchart.pdf)
 
HTML5 makes it easy to make your site accessible to users with disabilities. Once you understand how to properly use the HTML5 semantic elements and learn how assistive technologies work, designing your site with accessibility in mind becomes even easier!

