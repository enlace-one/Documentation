# Alignment

## Side by Side with Inline
```html
<div>
    <h1 style="display: inline-block;">
        Title
    </h1>
    <p style="display: inline-block;">
        Menu
    </p>
</div>
```

## Using Grid
The below shows as three columns on large screens and three rows on small ones. 
```css
.header-grid {
    display: grid;
    grid-template-areas:
        "header"
        "menu"
        "search";
}

@media (min-width: 650px) {
    .header-grid {
        display: grid;
        grid-template-areas: "header menu search";
    }
}
```
```html
 <div class=".header-grid">
  <div style="grid-area: header">1</div>
  <div cstyle="grid-area: menu">2</div>
  <div style="grid-area: search">3</div>
</div> 
```

