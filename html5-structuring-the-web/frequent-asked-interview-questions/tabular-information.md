# Tabular information

## Not very common tabular tags in HTML.

### Adding a caption to your table with `<caption>`

A caption is placed directly beneath the `<table>` tag.

```markup
<table>
  <caption>Dinosaurs in the Jurassic period</caption>
  <!-- ... -->
</table>
```

### Adding structure with `<thead>`, `<tfoot>`, and `<tbody>`

* The `<thead>` element must wrap the part of the table that is the header — this is usually the first row containing the column headings, but this is not necessarily always the case. If you are using [`<col>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/col)/[`<colgroup>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/colgroup) element, the table header should come just below those.
* The `<tfoot>` element needs to wrap the part of the table that is the footer — this might be a final row with items in the previous rows summed, for example. You can include the table footer right at the bottom of the table as you'd expect, or just below the table header (the browser will still render it at the bottom of the table).
* The `<tbody>` element needs to wrap the other parts of the table content that aren't in the table header or footer. It will appear below the table header or sometimes footer, depending on how you decided to structure it.

## The real challenge of handle a HTML `table`

> There are a few other things you could learn about table HTML, but we have really given all you need to know at this moment in time. At this point, you might want to go and learn about styling HTML tables.

### Sizing table

One tip for size table automatically, is don't give any certain width to any cells. It helps you to layout and adjust your table in a certain balance. But, this is not a good solution in responsive design anyway.

And, giving the table a certain width is always a bad choice to make.

To improve the UX in data presentation by a table. Always focus on useful and valid data. A good tip is use a dash to present some data is not worked.

If the data or the text in a single cells is too long. Always remember to use the CSS attribute [`ellipsis`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow) to show the content and use something like a [popover](https://getbootstrap.com/docs/4.0/components/popovers/) to show the detail.&#x20;
