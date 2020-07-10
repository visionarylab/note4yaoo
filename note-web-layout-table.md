---
tags: [layout, table, web]
title: note-web-layout-table
created: '2020-07-10T02:40:36.658Z'
modified: '2020-07-10T08:38:36.261Z'
---

# note-web-layout-table

## guide

- ref
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table
  - https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Legacy_Layout_Methods
  - [Are CSS Tables Better Than HTML Tables? _2011](https://vanseodesign.com/css/tables/)
  - [CSS vs Tables: The Debate That Won’t Die_2009](http://vanseodesign.com/css/css-divs-vs-tables/)
  - [Why CSS should not be used for layout_2009](http://www.flownet.com/ron/css-rant.html)
  - [Why CSS Should Be Used for Layout_2009](https://www.newmediacampaigns.com/blog/why-css-should-be-used-for-layout)
  - [Slow response when the HTML table is big](https://stackoverflow.com/questions/8640692/slow-response-when-the-html-table-is-big)
  - [Are large html tables slow?](https://stackoverflow.com/questions/1364213/are-large-html-tables-slow)

## faq
- When should you NOT use HTML tables?
  - HTML tables should be used for tabular data — this is what they are designed for. 
    - Unfortunately, a lot of people used to use HTML tables to lay out web pages, 
    - e.g. one row to contain the header, one row to contain the content columns, one row to contain the footer, etc.
  - Layout tables reduce accessibility for visually impaired users 
    - Screenreaders, used by blind people, interpret the tags that exist in an HTML page and read out the contents to the user. 
    - Because tables are not the right tool for layout, and the markup is more complex than with CSS layout techniques, the screenreaders' output will be confusing to their users.
  - Tables produce tag soup
    - table layouts generally involve more complex markup structures than proper layout techniques. 
    - This can result in the code being harder to write, maintain, and debug.
  - Tables are not automatically responsive
    - When you use proper layout containers (such as `<header>, <section>, <article>, or <div>`), their width defaults to 100% of their parent element. 
    - Tables on the other hand are sized according to their content by default, so extra measures are needed to get table layout styling to effectively work across a variety of devices.

## pieces
- Tables have to be downloaded and render in full before they are displayed, appearing to take a longer to display. This lapse all depends on processing power. You can 
  - remove gradient backgrounds (as they are rendered by the browser)
  - paginate form data
  - output form rows in chunks (say, 200 rows at a time)
  - does removing all css help?
  - specify a exact width + height on table rows, cells
  - Set the table-layout CSS attribute to fixed on the table.
  - Explicitly define col objects for each column.
  - Set the WIDTH attribute on each col.

- A table is a structured set of data made up of rows and columns (tabular data). 
- A table allows you to quickly and easily look up values that indicate some kind of connection between different types of data
- HTML has a method of defining styling information for an entire column of data all in one place — the `<col>` and `<colgroup>` elements.
  - These exist because it can be a bit annoying and inefficient having to specify styling on columns
  - you generally have to specify your styling information on every `<td>` or `<th>` in the column, or use a complex selector such as `:nth-child()`.
  - Styling columns like this is limited to a few properties: `border`, `background`, `width`, and `visibility`. 
  - To set other properties, you'll have to either style every `<td>` or `<th>` in the column, or use a complex selector such as `:nth-child()`.
- Floated grid limitations
  - The biggest limitation of this system is that it is essentially one dimensional. 
    - We are dealing with columns, and spanning elements across columns, but not rows. 
    - It is very difficult with these older layout methods to control the height of elements without explicitly setting a height, 
    - and this is a very inflexible approach too — it only works if you can guarantee that your content will be a certain height.
  - When using a system like this you do need to take care that your total widths add up correctly, 
    - and that you don’t include elements in a row that span more columns than the row can contain. 
    - Due to the way floats work, if the number of grid columns becomes too wide for the grid, the elements on the end will drop down to the next line, breaking the grid.
    - Also bear in mind that if the content of the elements gets wider than the rows they occupy, it will overflow and look a mess.
- Flexbox was never designed as a grid system and poses a new set of challenges when used as one.
  - Flexbox is one-dimensional by design. 
    - It deals with a single dimension, that of a row or a column.
    - We can’t create a strict grid for columns and rows, meaning that if we are to use flexbox for our grid, we still need to calculate percentages as for the floated layout.
- In your project you might still choose to use a flexbox ‘grid’ due to the additional alignment and space distribution capabilities flexbox provides over floats. 
- You should, however, be aware that you are still using a tool for something other than what it was designed for. So you may feel like it is making you jump through additional hoops to get the end result you want.
- All Skeleton (or any other grid framework) is doing is setting up predefined classes that you can use by adding them to your markup. It’s exactly the same as if you did the work of calculating these percentages yourself.
- Assistive technology such as screen readers may have difficulty parsing tables that are so complex that header cells can’t be associated in a strictly horizontal or vertical way. 
  - This is typically indicated by the presence of the `colspan` and `rowspan` attributes.
  - Ideally, consider alternate ways to present the table's content, including breaking it apart into a collection of smaller, related tables that don't have to rely on using the `colspan` and `rowspan` attributes.
  - If the table cannot be broken apart, use a combination of the `id` and `headers` attributes to programmatically associate each table cell with the header(s) the cell is associated with.

## Are CSS Tables Better Than HTML Tables
- The css table model is based on the html4 table model and has pretty good browser support. 
- In both table models, the table structure parallels the visual display of the table itself.
- Rows are primary. The row is specified explicitly and columns are derived from how the rows and cells are set up.
- Each html table element has an equivalent css display value. The only real difference is that there’s no distinction between td and th with the css variety.
- Below are the html table elements and their corresponding css display value.
``` css
table     { display: table }
tr        { display: table-row }
thead     { display: table-header-group }
tbody     { display: table-row-group }
tfoot     { display: table-footer-group }
col       { display: table-column }
colgroup  { display: table-column-group }
td, th    { display: table-cell }
caption   { display: table-caption }
```
- Looking at the above it shouldn’t be too hard to figure out how to set up a css table.

``` html
<div id="table">
  <div class="row">
    <span class="cell"></span>
    <span class="cell"></span>
     <span class="cell"></span>
  </div>
  <div class="row">
    <span class="cell"></span>
    <span class="cell"></span>
     <span class="cell"></span>
  </div>
  <div class="row">
    <span class="cell"></span>
    <span class="cell"></span>
     <span class="cell"></span>
  </div>
</div>

```

``` css

#table {display: table;}
.row {display: table-row;}
.cell {display: table-cell;}
```
- If you look only at the html above, you can easily see the basic table structure except that I’ve used `div and span` with ids and classes instead of `table, tr, and td`.
- Different table elements have different stacking contexts for the purpose of adding backgrounds to these different layers.
  1. table – lowest layer
  2. column group
  3. columns
  4. row group
  5. rows
  6. cells – highest layer
- The background of any layer will only be seen if all the layers above it have backgrounds set to transparent.
- The width of css tables can be calculated using one of two algorithms. 
- The `table-layout` CSS property sets the algorithm used to lay out `<table>` cells, rows, and columns.
  - `auto`
    - By default, most browsers use an automatic table layout algorithm. 
    - The widths of the table and its cells are adjusted to fit the content.
    - The width of table is set by width of columns and borders
  - `fixed`
    - Table and column widths are set by the widths of table and col elements or by the width of the first row of cells. 
    - Cells in subsequent rows do not affect column widths.
    - Under the `fixed` layout method, the entire table can be rendered once the first table row has been downloaded and analyzed. 
      - This can speed up rendering time over the "automatic" layout method, but subsequent cell content might not fit in the column widths provided. 
      - Cells use the overflow property to determine whether to clip any overflowing content, but only if the table has a known width; otherwise, they won't overflow the cells.
    - The width of the layout is not determined by its content, but rather by the widths set on the table, cells, borders, and/or cell spacing
- The important thing to consider is that a `fixed` table-layout is a one-pass calculation and very quick. 
- On the other hand `auto` requires the same multiple passes of html tables. It’s also the default value.
- If you explicitly set a `width` on the table, then the fixed table layout algorithm will be used.
- By default the cell `height` will be the minimum necessary to display the contents of the cell, 
  - but you can also explicitly set heights. 
  - All cells in a row will be the height of the cell with the maximum minimum necessary height.
- The `vertical-align` property of each table cell determines the cell’s alignment within the row
- css table borders
- `border-collapse` — values can be collapse, separate, or inherit
- `border-spacing` — values can be horizontal length  vertical length, or inherit. 
  - border-spacing is the distance between cell borders.
- `empty-cells` — values can be show, hide, or inherit. 
  - If cells are empty or set to `visibility: hidden` content doesn’t show by default. 
  - Setting `empty-cells: show` on the table will cause backgrounds and borders to display for the empty cell.
- Cons for using html tables for layout over a combination of divs and css.
  - Extra code
    - html tables require more structural code than divs, but css tables use just as much. 
    - If anything css tables use more since ids and classes will likely be added. 
    - If html tables use too much code then css tables do too.
  - Rigid structure
    - html tables are source dependent. 
    - The order you structure the cells is the same order in which they’ll display. 
    - The same is essentially true of css tables as well.
  - Browser rendering
    - browsers require multiple passes at the structure of html tables. 
    - They should only require one pass to display a css table if the table-layout is set to fixed. 
    - They’ll require the same multiple passes if set to auto.
- Considering the above, css tables aren’t offering enough benefit over html tables to use them for layout.
- CSS tables do have the advantage of being more semantically correct, as we can choose html elements that better describe our content.
- Overall it’s hard for me to see much improvement in css tables over html tables, some perhaps, but not enough to justify to myself using them.
- There are two arguments for CSS tables that haven’t been made (or I missed them):
  - You can enclose (CSS-) table rows in their own form, which is helpful if you want to make a CRUD-like table with editable rows.
    - If you have one form per row, only the input in the selected row will be submitted; 
    - with HTML tables you can only enclose the entire table in a form and you’ll then have to figure out on the server side what row has been edited (not to mention an unnecessary large POST if you have a large table).
  - You can create a responsive layout without needing Javascript and e.g. resize or hide columns depending on the device size.
    - Or you can split rows: for example, for very narrow devices you might want to switch the table to a single column layout simply by removing or replacing the “display: table*” style without generating different HTML for that case.

## CSS vs Tables: The Debate That Won’t Die
- One of the debates that never seems to go away in the web development community is that of css vs tables and which is better to use for the layout of your site.
- I do think css is the better option, but feel free to develop sites any way you want.
- What the css vs tables debate is really about is whether or not to structure a web page with tables or divs. In its simplest form we’re comparing:
``` html
<table>
  <tr>
    <td>Some content here</td>
  </tr>
</table>

<!-- vs -->

<div>Some content here</div>
```

- tables are a more complex structure than divs. 
  - As we add more to the page’s design, the table complexity continues to increase compared to divs.
  - Every table cell is dependent on the other table cells in its row to maintain the structure. Divs can work independently from each other. Using table makes it not easy to move dom elements
  - The third problem with tables is in how browsers render them. 
    - In order for a browser to render a page built with tables, it needs to read the code on the page twice. 
    - Once to understand the structure and another time to present it. 
    - That extra pass at the code makes table-based layouts take longer to display. 
    - With a simple table structure, the extra time might not be noticeable, 
    - but as the structure becomes more complex with more and more tables nested inside each other it is noticeable.
- A div-based layout is:
  - easier to maintain
    - less code and less complexity to the structure makes things easier to find and change.
  - more flexible
    - since one div is not dependent on the other divs on the page it allows for more freedom in your design
  - quicker to load 
    - blocks of code can be presented right away instead of the browser requiring an extra pass
- CSS (divs) are better for SEO?
  - Search engines don’t care one bit if the code behind your page uses tables or divs. 
  - Search engines are interested in your content, not your code. 
  - It’s true that less code means less potential for show stopping errors, but those show stoppers can exist regardless of your site’s structure.
  




