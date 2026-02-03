# Color System Documentation

The BFHCF website uses a centralized color system defined in multiple locations for different purposes.

## Color Definitions

### Data File (_data/colors.yml)
Contains color definitions that can be accessed in Liquid templates via `site.data.colors`.

### SCSS Variables (assets/css/custom/_variables.scss)
SCSS variables used in stylesheets for compilation. These must match the data file values.

### CSS Classes (assets/css/custom/_colors.scss)
Generated utility classes for:
- Text colors: `.color-bfhcf-{color}`, `.color-bfhcf-{color}-light`
- Background colors: `.bg-bfhcf-{color}`
- Card hover states: `.card-bfhcf-{color}`

## Available Colors

- **red**: #ff5139
- **green**: #58c31e
- **teal**: #3b8686
- **purple**: #906090
- **yellow**: #ffdf3e
- **orange**: #fea51b
- **cyan**: #00cbcb
- **lime**: #a1de45
- **black**: #000000

## Usage

### In Liquid Templates
```liquid
{% for color in site.data.colors %}
  <div style="background-color: {{ color.hex }}">{{ color.name }}</div>
{% endfor %}
```

### In HTML
```html
<h1 class="color-bfhcf-teal">Title</h1>
<div class="bg-bfhcf-purple">Content</div>
```

### In SCSS
```scss
.my-element {
  color: $bfhcf-cyan;
  background-color: $bfhcf-orange;
}
```

## Maintenance

When adding or modifying colors:
1. Update `_data/colors.yml`
2. Update `assets/css/custom/_variables.scss`
3. Optionally add new utility classes in `assets/css/custom/_colors.scss`
