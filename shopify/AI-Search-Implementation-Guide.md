**AI Search**

Implementation Guide for Shopify

*Step-by-step setup instructions for new clients*

Component hosted on CDN · No file uploads required

# **Overview**

AI Search adds a Search with AI button to your blog page. Clicking it opens a full-screen modal where visitors can type a query, press Enter, and instantly see blog posts ranked by meaning — not just keyword matches.

The component is delivered as a single JavaScript file hosted on a CDN. You do not need to upload or manage any JS or CSS files. You only need to:

* Add one script tag to load the component from the CDN

* Place the \<lw-ai-search\> element in your liquid file on shopify

* Pass your credentials and styling preferences as HTML attributes

# **Prerequisites**

* Access to your Shopify theme's code editor — Admin → Online Store → Themes → Edit code

* Your three credentials (provided by your contact at LevelWorks):
    -  Backend URL    e.g.   https://example.com  
    -  API Key             e.g.  pk\_live\_abc123...
    -  Search Index   e.g.  all 


## 

## **Step 1 — Open the Theme Code Editor**

1. Go to your Shopify Admin

2. Click Online Store in the left sidebar

3. Click Themes

4. Next to your active theme, click the "..." button → Edit code

You will see a file explorer on the left with folders like Assets, Sections, and Templates.

## **Step 2 — Find Your Blog Section File**

You need to edit the section file that controls your blog listing page. To find it:

5. Open Templates → blog.json

6. Look for the "type" field of the main section — for example:  "type": "custom-blog"

7. Open that file from Sections — e.g. custom-blog.liquid

ℹ  *This is the file you will edit in Steps 3 and 4\.*

## **Step 3 — Add the CDN Script Tag**

At the very top of your blog section file, add this line to load the component:
```
\<script type="module"
  src="https://cdn.jsdelivr.net/gh/levelworksco/cdn@main/lw-ai-search/shopify/lw-ai-search.js"\>
\</script\>
```

ℹ  *The type="module" attribute is required. Without it the component will not load.*

## **Step 4 — Place the Component in Your Template**

Inside the same file, add the \<lw-ai-search\> element wherever you want the button to appear — typically in your sidebar. Replace the three credential values with your own:

```
\<lw-ai-search class="lw-ai-search"
  search-base="https://your-backend-url.com"
  search-key="your\_api\_key"
  search-index="All"
  btn-label="Search with AI"
  btn-subtext="Ask anything to find relevant blogs"
\>\</lw-ai-search\>
```

The class="lw-ai-search",(or any other name you prefer) is optional but recommended — it lets you target the component with CSS later (see Step 6).

## **Step 5 — Configure the Button with HTML Attributes**

All visual properties of the button, container, and subtext can be controlled by passing attributes directly on the \<lw-ai-search\> tag. No CSS file editing is needed for these.

**Credentials (required)**

| Attribute | Description |
| :---- | :---- |
| search-base | Your backend URL. e.g. https://example.com |
| search-key | Your API key. e.g. pk\_live\_abc123... |
| search-index | Your search index name. e.g. all |

**Button appearance (optional: all css properties have a fallback)**

| Attribute | Default | Effect |
| :---- | :---- | :---- |
| btn-label | Search with AI | Text shown on the button |
| btn-background | \#f58220 | Button background colour |
| btn-hover-background | \#d16e19 | Background colour on hover |
| btn-color | \#ffffff | Button text/icon colour |
| btn-width | 100% | Button width |
| btn-height | auto | Button height |
| btn-padding | 14px | Button padding |
| btn-border-radius | 6px | Button corner radius |
| btn-font-size | 16px | Button label font size |
| btn-font-weight | 500 | Button label font weight |
| btn-icon-size | 16px | Size of the sparkle icon |
| btn-gap | 5px | Gap between icon and label |

**Subtext (the line below the button)**

| Attribute | Default | Effect |
| :---- | :---- | :---- |
| btn-subtext | Ask anything... | Subtext content |
| btn-subtext-color | \#777 | Subtext colour |
| btn-subtext-font-size | 12px | Subtext font size |
| btn-subtext-margin-top | 8px | Space between button and subtext |

**Container (the wrapper around button and subtext)**

| Attribute | Default | Effect |
| :---- | :---- | :---- |
| container-width | 220px | Width of the whole component |
| container-margin | 0 | Outer margin |
| container-padding | 0 | Inner padding |
| container-text-align | center | Text alignment inside container |
| container-display | block | CSS display value |
| container-align-items | initial | Flexbox align-items |
| container-justify-content | initial | Flexbox justify-content |
| container-flex-direction | initial | Flexbox flex-direction |
| container-gap | initial | Gap between flex children |

## **Step 6 — Advanced Styling with CSS ::part()**

For any styling not covered by the attributes above, you can target elements inside the component from your blog page's CSS file using the ::part() selector. This is the standard way to style Web Component internals.

Here is the HTML structure rendered by the component, showing each element's class and part name:

```
\<div class="ai-search-container"  part="ai-search-container"\>
  \<button class="ai-search-btn"    part="ai-search-btn"\>
    \<div class="inner-container"   part="inner-container"\>
      \<svg class="btn-icon"        part="btn-icon"\> ... \</svg\>
      Search with AI
    \</div\>
  \</button\>
  \<p class="ai-search-subtext"    part="ai-search-subtext"\>
    Ask anything to find relevant blogs
  \</p\>
\</div\>
```
The following parts are exposed:

| Part name | Element it targets |
| :---- | :---- |
| ai-search-btn | The button element itself |
| ai-search-subtext | The paragraph below the button |
| ai-search-container | The wrapper div around button and subtext |
| inner-container | The flex row inside the button (icon \+ label) |
| btn-icon | The SVG sparkle icon inside the button |

Example — add these to your custom-blog.css file:
```
.lw-ai-search::part(ai-search-btn) {
  background: \#000000;
  border-radius: 999px;
}

.lw-ai-search::part(ai-search-subtext) {
  text-decoration: underline;
  color: \#f58220;
}

.lw-ai-search::part(ai-search-container) {
  border: 1px solid \#eee;
  padding: 12px;
}
```
ℹ  *The class="lw-ai-search" on the element (added in Step 4\) is what makes the .lw-ai-search selector work. Without it, the ::part() rules will not apply.*

## **Step 7 — Test It**

8. Save your files

9. Visit your store's blog page — e.g. yourstore.com/blogs/all

10. You should see the Search with AI button

11. Click it — the full-screen search modal should open

12. Type a query and press Enter — results should appear

13. Press Escape, click ×, or click the dark backdrop to close

# **How It Works**

* **On page load:** The script tag loads the component from the CDN. No file is stored in your theme.

* **Component mount:** The \<lw-ai-search\> tag renders the button and subtext. The modal is invisible until triggered.

* **Button click:** Clicking the button opens the modal and focuses the search input.

* **Search trigger:** Nothing happens until the user types a query and presses Enter. Empty queries are ignored.

* **Search as you type:** After the first search, results update automatically as the user keeps typing, with a 350ms debounce.

* **Navigation:** Clicking a result opens the blog post. The browser back button returns to the modal with results intact.

* **Closing:** Close by clicking ×, clicking the dark backdrop, or pressing Escape.

# **Full Example**

This is a complete snippet showing all attributes. Paste it into your blog section file, replacing credential values with your own.
```
\<script type="module"
  src="https://cdn.jsdelivr.net/gh/levelworksco/cdn@main/lw-ai-search/shopify/lw-ai-search.js"\>
\</script\>
```

```
\<lw-ai-search class="lw-ai-search"
  search-base="https://discoverai.levelworks.co"
  search-key="pk\_live\_your\_key\_here"
  search-index="All"
  btn-label="Search with AI"
  btn-background="\#f58220"
  btn-color="\#ffffff"
  btn-width="220px"
  btn-border-radius="6px"
  btn-font-size="16px"
  btn-subtext="Ask anything to find relevant blogs"
  btn-subtext-color="\#777"
  container-width="220px"
  container-text-align="center"
\>\</lw-ai-search\>
```
# **Troubleshooting**

| Problem | Likely Cause | Fix |
| :---- | :---- | :---- |
| Button appears but modal doesn't open | Component not loaded | Check Step 3 — ensure the script tag has type="module" |
| Modal opens but no results appear | Wrong credentials | Double-check search-base, search-key, and search-index attributes |
| Button style attributes are not applying | Typo in attribute name | Check attribute names exactly as listed in Step 5 |
| ::part() styles are not applying | Missing class on the element | Ensure class="lw-ai-search" is on the \<lw-ai-search\> tag |
| Nothing appears at all | Wrong template file edited | Check Step 2 — confirm you edited the file that renders your blog page |
| Component broken after theme update | Theme update overwrote liquid file | Re-add the script tag and element to the blog section file |

# **Files Reference**

There are no files to upload. The only files you touch are existing files in your theme:

| File | Location | What you do |
| :---- | :---- | :---- |
| custom-blog.liquid (or equivalent) | Sections | Add the script tag and \<lw-ai-search\> element |
| custom-blog.css (or equivalent) | Assets | Optionally add ::part() styles for advanced customisation |
| blog.json | Templates | Points to your blog section — no changes needed here |

