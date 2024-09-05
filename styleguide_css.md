A personal style guide to keep CSS consistent.

# General Guidelines
1. Use variables for colors and common sizes
2. Styles use more than once go in a shared .css file
3. Elements with more than three `style` attributes can't use inline style
4. Each .html file on the development end may have up to one `<style>` tag
5. Class and ID names shall follow this format: `class-name`
6. Don't use CSS shorthand

## Units and When to Use What
### Units - rems
Use these units for:
- Font Size

### Units - percentages and viewport units
Use these units when things need to resize themselves

### Units - pixels
Use these for:
- Padding
- Margin
- Border-width
