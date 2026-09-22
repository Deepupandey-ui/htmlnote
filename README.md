HTML — Complete Notes (Basics → Advanced)
For Notebook Writing | MERN Interview Prep | Professional Development (2026)
1. What is HTML?
HTML (HyperText Markup Language) — the standard markup language (not a programming language) used to structure content on the web.

HyperText → text containing links to other text (hypertext links / hyperlinks)
Markup Language → uses tags to define elements within a document
Current version: HTML5 (maintained by WHATWG, spec published as a "Living Standard")
Works with CSS (styling) and JavaScript (behavior) → the 3 pillars of front-end web dev
Interview Q: Is HTML a programming language? No — it has no logic, loops, or conditionals. It's a markup/declarative language describing structure.

2. Basic Document Structure (Boilerplate)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
Part	Purpose
<!DOCTYPE html>	Tells browser to render in standards mode (HTML5). Not an HTML tag itself.
<html>	Root element; lang attribute helps SEO + screen readers
<head>	Metadata — not visible on page (title, meta, links, styles, scripts)
<meta charset="UTF-8">	Character encoding — supports all languages/symbols
<meta name="viewport">	Makes page responsive on mobile devices
<body>	Visible page content
Interview Q: Quirks mode vs Standards mode? Missing/incorrect <!DOCTYPE> → browser renders in Quirks Mode (legacy, inconsistent CSS box model behavior across browsers). With correct doctype → Standards Mode (spec-compliant rendering).

3. HTML Elements & Tags — Core Concepts
Tag: <p> (opening), </p> (closing)
Element: opening tag + content + closing tag → <p>Text</p>
Void/Self-closing elements (no closing tag, no content): <br>, <hr>, <img>, <input>, <meta>, <link>, <source>, <col>, <area>, <embed>, <wbr>
Nesting must be proper: <b><i>text</i></b> ✅ not <b><i>text</b></i> ❌
Comments: <!-- comment --> (not rendered, visible in source)
Block vs Inline Elements
Block-level	Inline
Starts on a new line, takes full width available	Flows within text, takes only needed width
Can contain block + inline elements	Can generally only contain other inline elements/text
<div>, <p>, <h1>-<h6>, <ul>, <li>, <section>, <form>, <table>	<span>, <a>, <strong>, <em>, <img>, <label>, <b>, <i>
Respects width/height/margin fully	width/height often ignored unless display changed
Interview Q: <div> vs <span>? <div> = block-level generic container (layout/grouping). <span> = inline generic container (styling a piece of text/inline content).

4. Attributes
Attributes provide extra information about an element — always in the opening tag, name="value" pairs.

Global Attributes (usable on almost any element)
Attribute	Use
id	Unique identifier (used once per page; CSS #id, JS getElementById)
class	Non-unique, reusable identifier (CSS .class, can apply to many elements)
style	Inline CSS (avoid in production — poor separation of concerns)
title	Tooltip text on hover
data-*	Custom data attributes e.g. data-user-id="123" → accessed via JS element.dataset.userId
hidden	Hides element (display:none equivalent)
tabindex	Controls keyboard tab order
contenteditable	Makes element editable by user
draggable	Enables HTML5 drag-and-drop
lang, dir	Language and text direction (ltr/rtl)
spellcheck	Enable/disable browser spellcheck
Interview Q: id vs class?

id	class
Unique — one per page	Reusable across multiple elements
CSS specificity: higher	CSS specificity: lower
#idName	.className
JS: getElementById (single)	JS: getElementsByClassName / querySelectorAll (multiple)
5. Text & Formatting Elements
<h1> to <h6>     <!-- headings, h1 = most important (1 per page ideally, SEO) -->
<p>              <!-- paragraph -->
<br>             <!-- line break (void) -->
<hr>             <!-- thematic break / horizontal rule (void) -->
<strong>         <!-- important text — bold + semantic weight -->
<b>              <!-- bold — visual only, no semantic meaning -->
<em>             <!-- emphasized text — italic + semantic stress -->
<i>              <!-- italic — visual only -->
<mark>           <!-- highlighted text -->
<small>          <!-- fine print -->
<del>            <!-- deleted/strikethrough text -->
<ins>            <!-- inserted/underlined text -->
<sub> / <sup>    <!-- subscript / superscript -->
<blockquote>     <!-- long quotation (block) -->
<q>              <!-- short inline quotation -->
<cite>           <!-- title of a work -->
<code>           <!-- inline code snippet -->
<pre>            <!-- preformatted text, preserves whitespace -->
<abbr title="...">  <!-- abbreviation with tooltip -->
Interview Q: <strong> vs <b>, <em> vs <i>? <strong>/<em> carry semantic meaning (read differently by screen readers, affect SEO). <b>/<i> are purely presentational with no semantic weight. Always prefer semantic tags.

6. Lists
<ul>                     <!-- unordered list -->
  <li>Item</li>
</ul>

<ol type="1" start="1" reversed>   <!-- ordered list -->
  <li>Item</li>
</ol>

<dl>                     <!-- description/definition list -->
  <dt>Term</dt>
  <dd>Description</dd>
</dl>
Lists can be nested (list inside <li>)
<ol> attributes: type (1, A, a, I, i), start, reversed
7. Links (Anchor Tag)
<a href="https://example.com" target="_blank" rel="noopener noreferrer" download title="tip">Link</a>
Attribute	Purpose
href	Destination URL (can be absolute, relative, #id for same-page anchor, mailto:, tel:)
target="_blank"	Opens in new tab
rel="noopener noreferrer"	Security: prevents new tab from accessing window.opener (tabnabbing protection) — must-know for interviews
download	Forces file download instead of navigation
Interview Q: Why use rel="noopener" with target="_blank"? Without it, the opened page can access window.opener and redirect the original tab — a phishing/security risk ("tabnabbing"). Modern browsers auto-apply noopener by default now, but it's still asked frequently.

Relative vs Absolute URL

Absolute	Relative
Full path: https://site.com/page	Path from current file: ../images/pic.png
Works anywhere	Depends on file structure
8. Images & Media
<img src="img.jpg" alt="description" width="300" height="200" loading="lazy">

<picture>
  <source media="(min-width:800px)" srcset="large.jpg">
  <source media="(min-width:400px)" srcset="medium.jpg">
  <img src="small.jpg" alt="fallback">
</picture>

<img srcset="small.jpg 480w, large.jpg 1080w" sizes="(max-width:600px) 480px, 1080px" src="large.jpg" alt="...">
Attribute	Why it matters
alt	Critical — accessibility (screen readers) + SEO + fallback if image fails to load
loading="lazy"	Native lazy-loading — big performance win, no JS library needed (2026 best practice)
width/height	Prevents Cumulative Layout Shift (CLS) — Core Web Vitals metric
srcset/sizes	Responsive images — browser picks best resolution for device
<picture>	Art direction — different images/crops per breakpoint (vs srcset which is same image, different resolutions)
Interview Q: <picture> vs srcset? srcset = same image at different resolutions (bandwidth optimization). <picture> = different image sources entirely for different conditions (art direction), browser picks first matching <source>.

9. Tables
<table>
  <caption>Table Title</caption>
  <thead>
    <tr><th>Name</th><th>Age</th></tr>
  </thead>
  <tbody>
    <tr><td>Deepu</td><td colspan="2">22</td></tr>
  </tbody>
  <tfoot>
    <tr><td>Total</td><td>1</td></tr>
  </tfoot>
</table>
colspan → merges cells horizontally
rowspan → merges cells vertically
<thead>, <tbody>, <tfoot> → semantic table sections (help styling + accessibility + printing)
Tables should be used for tabular data only — never for page layout (old, deprecated practice)
10. Forms (Heavy Interview Topic)
<form action="/submit" method="POST" enctype="multipart/form-data" autocomplete="off" novalidate>

  <label for="email">Email</label>
  <input type="email" id="email" name="email" required placeholder="you@mail.com">

  <input type="password" name="pwd" minlength="8" pattern="[A-Za-z0-9]+">
  <input type="number" name="age" min="1" max="100" step="1">
  <input type="checkbox" name="agree" checked>
  <input type="radio" name="gender" value="m">
  <input type="file" name="doc" accept=".pdf,.docx" multiple>
  <input type="date">
  <input type="range" min="0" max="10">
  <input type="hidden" name="token" value="xyz">
  <input type="search">
  <input type="color">

  <select name="country">
    <optgroup label="Asia">
      <option value="in">India</option>
    </optgroup>
  </select>

  <textarea rows="4" cols="30" maxlength="200"></textarea>

  <fieldset>
    <legend>Personal Info</legend>
    ...
  </fieldset>

  <button type="submit">Submit</button>
  <button type="reset">Reset</button>
  <button type="button">Just a button (no default action)</button>
</form>
All <input> types worth memorizing:
text, password, email, number, tel, url, search, date, time, datetime-local, month, week, color, range, checkbox, radio, file, hidden, submit, reset, button, image

Form Validation Attributes
Attribute	Effect
required	Field must be filled
minlength / maxlength	Text length constraints
min / max / step	Numeric/date constraints
pattern	Regex validation
novalidate (on <form>)	Disables browser's native validation
disabled	Field not editable, not submitted with form
readonly	Field not editable, but submitted with form
Interview Q: disabled vs readonly? disabled → value not sent on submit, cannot be focused/edited. readonly → value IS sent on submit, cannot be edited but can be focused/selected/copied.

Interview Q: GET vs POST method?

GET	POST
Data appended in URL (query string)	Data sent in request body
Limited data size, visible in URL	No size limit (practically), hidden from URL
Cacheable, bookmarkable	Not cached by default
Used for fetching/reading data	Used for submitting sensitive/large data
Idempotent	Not idempotent
Interview Q: <label for=""> importance? Associates label with input → clicking label focuses/activates input; critical for accessibility (screen readers announce the label).

Form UX/label association — two ways:
<label for="name">Name</label><input id="name">
<!-- OR -->
<label>Name <input></label>
11. Semantic HTML5 Elements (Very Important — SEO + Accessibility + Interviews)
<header>   <!-- introductory content / site header -->
<nav>      <!-- navigation links -->
<main>     <!-- main unique content of page (only ONE per page) -->
<section>  <!-- thematic grouping of content, usually with a heading -->
<article>  <!-- self-contained, independently distributable content (blog post, news card) -->
<aside>    <!-- tangential content, sidebars -->
<footer>   <!-- footer content -->
<figure> / <figcaption>  <!-- self-contained media with caption -->
<time datetime="2026-09-22">Sept 22</time>  <!-- machine-readable date/time -->
<details> / <summary>    <!-- native collapsible widget, no JS needed -->
<dialog>   <!-- native modal dialog -->
Why semantic HTML matters (frequently asked):

Accessibility — screen readers navigate by landmarks (nav, main, etc.)
SEO — search engines weigh semantic structure for ranking
Maintainability — self-documenting code vs <div class="header"> soup
Consistent browser behavior (e.g., <details> native toggle)
Interview Q: <section> vs <div>? <section> is semantic — used for thematic content grouping, ideally with a heading. <div> is a generic, non-semantic container used purely for styling/layout hooks.

Interview Q: <article> vs <section>? <article> = independently distributable/reusable (makes sense standalone — e.g., blog post, widget). <section> = grouped content within a page that isn't meant to stand alone.

12. Multimedia & Embedded Content
<audio controls autoplay loop muted>
  <source src="audio.mp3" type="audio/mpeg">
</audio>

<video controls width="400" poster="thumb.jpg">
  <source src="video.mp4" type="video/mp4">
  <track src="subs.vtt" kind="subtitles" srclang="en">
</video>

<iframe src="https://example.com" title="desc" loading="lazy" sandbox></iframe>

<canvas id="c" width="200" height="100"></canvas>   <!-- pixel-based, JS-drawn graphics -->

<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" />
</svg>
Interview Q: <canvas> vs <svg>?

Canvas	SVG
Pixel-based (bitmap), drawn via JS	Vector-based (XML), scalable without quality loss
Not part of DOM (single element, can't inspect shapes)	Each shape is a DOM node — inspectable, stylable via CSS
Better for many objects / games / real-time rendering	Better for icons, charts, logos, resolution independence
Interview Q: <iframe> vs <embed> vs <object>? <iframe> = embeds another full HTML document/page. <embed> = embeds external content/plugin (no closing tag, minimal fallback support). <object> = embeds external resources (PDF, media) with fallback content support between tags. <iframe> is by far the most used today.

13. <head> Metadata & SEO Essentials
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="description" content="Page summary for search engines">
<meta name="keywords" content="html, css, js">
<meta name="robots" content="index, follow">
<meta property="og:title" content="Open Graph title for social sharing">
<link rel="stylesheet" href="style.css">
<link rel="icon" href="favicon.ico">
<link rel="canonical" href="https://example.com/page">
<script src="app.js" defer></script>
<script> loading: normal vs async vs defer
Normal	async	defer
HTML parsing	Pauses while script downloads+executes	Continues while downloading; pauses to execute	Continues; script executes after parsing complete
Execution order	In order	Not guaranteed (whichever loads first)	In order (document order)
Best for	Small critical inline scripts	Independent scripts (analytics)	Scripts needing full DOM (most app scripts)
(This diagram-style table is one of the most common front-end interview questions.)

14. HTML Entities
Used to display reserved/special characters:

Entity	Renders	Entity	Renders
&lt;	<	&gt;	>
&amp;	&	&quot;	"
&copy;	©	&nbsp;	(non-breaking space)
&#169;	© (numeric)	&trade;	™
15. Accessibility (a11y) — Increasingly Asked in 2026 Interviews
Always use semantic tags over <div>/<span> where possible
alt text mandatory on meaningful images (empty alt="" for decorative images)
ARIA attributes when semantic HTML isn't enough:
role="button", aria-label="Close", aria-hidden="true", aria-expanded="true", aria-live="polite"
Keyboard navigability: all interactive elements reachable via Tab, use tabindex carefully
Sufficient color contrast, don't rely on color alone to convey meaning
Form inputs must have associated <label>s
Rule of thumb: "No ARIA is better than bad ARIA" — use native semantic HTML first.
16. HTML5 vs HTML4 — What's New
HTML4	HTML5
No semantic tags (<div id="header">)	Semantic tags (<header>, <nav>, <article>...)
Needed Flash/plugins for audio-video	Native <audio>, <video>
No client storage (only cookies)	localStorage, sessionStorage, IndexedDB
No canvas/SVG native support	Native <canvas>, inline <svg>
Complex DOCTYPE declaration	Simple <!DOCTYPE html>
No form validation attributes	required, pattern, type=email, etc.
No geolocation/drag-drop APIs	Geolocation API, Drag & Drop API
No Web Workers/WebSockets	Web Workers (background threads), WebSockets (real-time)
17. HTML5 APIs Worth Knowing (Conceptual, JS-driven)
API	Purpose
localStorage	Persistent key-value storage, ~5-10MB, no expiry, per-origin
sessionStorage	Same as localStorage but cleared when tab closes
Cookies	Small (~4KB), sent to server with every HTTP request, can have expiry
IndexedDB	Client-side database for large structured data
Geolocation API	navigator.geolocation.getCurrentPosition()
Drag and Drop API	draggable="true", ondragstart, ondrop
Web Workers	Run JS in background thread (no DOM access) — avoids blocking UI
WebSockets	Full-duplex, real-time client-server communication
History API	pushState/popState — enables SPA routing (core to React Router in MERN)
Interview Q: localStorage vs sessionStorage vs cookies?

localStorage	sessionStorage	cookies
Expiry	Never (until cleared)	On tab close	Set manually
Size	~5-10MB	~5-10MB	~4KB
Sent to server?	No	No	Yes, every request
Accessible from	Any tab, same origin	Same tab only	Any tab, same origin
18. Meta Viewport & Responsive Web Design Basics
<meta name="viewport" content="width=device-width, initial-scale=1.0">
width=device-width → matches screen's actual width (not desktop-scaled)
initial-scale=1.0 → 1:1 pixel ratio on load
Essential for mobile-first responsive design — without it, mobile browsers render at desktop width and zoom out
19. Important Differentiation Tables (Rapid Interview Revision)
HTML vs XHTML

HTML	XHTML
Lenient syntax (unclosed tags OK in practice)	Strict XML syntax — all tags must close, lowercase, quoted attributes
Forgiving parser	Must be well-formed XML
<script> in <head> vs before </body>

<head> (no defer/async)	Before </body>
Blocks HTML parsing/render	Loads after content is parsed → faster perceived load
Needs defer to avoid blocking	No attribute needed, but <head> + defer is the modern best practice
id selector vs data-* attribute

id	data-*
For unique identification + styling/JS hook	For storing custom data, not meant for styling
Void elements vs Normal elements

Void	Normal
No closing tag/content: <img>, <br>, <input>	Has opening + closing tag
20. HTML Document Parsing Flow (How Browser Builds the Page)
HTML file received

HTML Parser reads bytes -> tokens

Tokens converted to Nodes

DOM Tree constructed

CSS file received

CSSOM Tree constructed

DOM + CSSOM combined

Render Tree built

Layout / Reflow - calculate positions

Paint - pixels drawn on screen

Composite layers -> final page

Interview Q: Critical Rendering Path — what is it? The sequence of steps (above) the browser follows to convert HTML/CSS/JS into pixels on screen. Optimizing it (minifying CSS, deferring JS, avoiding render-blocking resources) is core to web performance.

21. HTML Best Practices for Professional / MERN Development (2026)
Always use semantic tags — improves SEO, accessibility, and code readability for team collaboration (React JSX also benefits from semantic structure).
One <h1> per page, proper heading hierarchy (h1→h2→h3, don't skip levels) — huge for SEO & accessibility.
Always add alt to images; use loading="lazy" for below-the-fold images.
Use <meta viewport> for responsive design always.
Keep JS non-blocking — use defer/async; in React, this is largely abstracted but the concept still matters for index.html.
Validate forms both client-side (required, pattern) and server-side (Node/Express) — never trust client-only validation.
Use rel="noopener noreferrer" with target="_blank" for security.
Minimize <div> soup — this maps directly to JSX component design in React (MERN's front end) — write meaningful, semantic component markup.
Ensure accessibility (label, aria-*, keyboard nav) — increasingly a hiring bar in 2026, some companies test for it explicitly.
Use <template> tag or React components (in MERN) instead of manually duplicating markup blocks.
Know that in React/JSX, class becomes className, for becomes htmlFor, attributes are camelCase (onClick, tabIndex) — this is a very common HTML→React interview bridge question.
22. Common Standalone Interview Questions (Quick-Fire)
What happens when you type a URL and hit enter? → DNS lookup → TCP/TLS handshake → HTTP request → server response → HTML parsing → DOM/CSSOM → render tree → paint.
Difference between HTML and HTML5? → See section 16 table.
What is the DOM? → Document Object Model — a tree-like, in-memory, language-independent representation of the HTML document that JS can manipulate.
Can you nest a <button> inside a <button>? → No, invalid HTML (interactive content cannot nest interactive content).
What is the difference between <link> and <a>? → <link> (in <head>) links external resources like CSS; <a> creates a hyperlink to navigate.
What is a self-closing tag and why does HTML5 not require the trailing slash? → e.g. <br> vs <br/> — HTML5 parser doesn't require XML-style self-closing; both work but <br> is standard HTML5.
What's the purpose of the alt attribute beyond accessibility? → SEO indexing + fallback display if image fails to load.
Difference between innerHTML, innerText, textContent? → (JS/DOM adjacent, often asked alongside HTML) innerHTML parses HTML tags; textContent gets all text including hidden elements, no parsing; innerText respects CSS visibility, triggers reflow (slower).
What is a semantic element? Give 5 examples. → See section 11.
Why is <!DOCTYPE html> necessary? → Prevents quirks mode; ensures standards-compliant rendering.
23. Quick Flow: Building a Typical Page Layout (Mental Model for MERN Devs)
html

head: meta, title, links

body

header: logo + nav

main

section: hero

section: content/article cards

footer

This structural thinking maps directly onto React component trees in a MERN app: <Header/>, <MainContent/>, <Footer/> — each internally using proper semantic HTML.

24. One-Page Summary Cheat Sheet (For Quick Revision Before Interview)
Markup language, not programming language
<!DOCTYPE html> → standards mode
Block vs inline elements
Semantic tags > divs for structure, SEO, accessibility
id (unique) vs class (reusable)
alt, label, aria-* → accessibility fundamentals
GET (URL, idempotent) vs POST (body, not idempotent)
defer vs async vs normal script loading
localStorage/sessionStorage/cookies differences
srcset/picture/loading="lazy" → responsive + performance
Void elements: img, br, hr, input, meta, link
Forms: validation attributes, disabled vs readonly
Canvas (pixel/JS) vs SVG (vector/DOM)
Critical Rendering Path: HTML→DOM, CSS→CSSOM→Render Tree→Layout→Paint
HTML5 additions: semantic tags, audio/video, canvas/svg, storage APIs, form types
Notes compiled for interview preparation and professional MERN-stack development — covers HTML fundamentals through advanced/modern (2026) practices.
