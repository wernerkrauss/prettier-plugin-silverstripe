# Prettier Silverstripe Plugin

A Prettier plugin for formatting Silverstripe CMS templates (`.ss` files).

This plugin allows Prettier to recognize and safely handle Silverstripe template tags (e.g., `<% if %>`, `<% loop %>`, `{$Variable}`) by masking them before passing the content to the HTML parser and unmasking them afterwards.

## Features

- Formats Silverstripe template files (`.ss`).
- Supports standard Silverstripe logic tags and variables.
- Works seamlessly with `prettier-plugin-tailwindcss` if installed.
- Preserves the structure of your templates while leveraging Prettier's HTML formatting power.

## Installation

Install the plugin via npm:

```bash
npm install --save-dev prettier-plugin-silverstripe
```

Or via yarn:

```bash
yarn add -D prettier-plugin-silverstripe
```

## Configuration

Add the plugin to your `.prettierrc` configuration file:

```json
{
  "plugins": ["prettier-plugin-silverstripe"],
  "overrides": [
    {
      "files": "*.ss",
      "options": {
        "parser": "silverstripe"
      }
    }
  ]
}
```

### Integration with Tailwind CSS

If you are using `prettier-plugin-tailwindcss`, this plugin will automatically detect it and use it to sort your Tailwind classes within the Silverstripe templates. Ensure both plugins are installed in your project.

```json
{
  "plugins": ["prettier-plugin-silverstripe", "prettier-plugin-tailwindcss"]
}
```

## Known Limitations

### "Tag Splitting"
Complex templates where HTML tags are split across Silverstripe logic tags can sometimes confuse the underlying HTML parser. 

**Example of what to avoid:**
```html
<% if $A %><div><% else %><section><% end_if %>
  Content
<% if $A %></div><% else %></section><% end_if %>
```

**Recommended approach:**
Instead of splitting tags, wrap the entire structure or use Includes to keep the HTML valid for the parser:
```html
<% if $A %>
  <div>Content</div>
<% else %>
  <section>Content</section>
<% end_if %>
```

## Development & Testing

If you want to contribute or run tests locally:

1. Clone the repository.
2. Run `npm install`.
3. Run `npm test` to execute the Jest test suite.

## License

[MIT](LICENSE)

## Need Help?

If you need some help with your Silverstripe project, feel free to [contact me](mailto:werner.krauss@netwerkstatt.at) ✉️.

See you at next [StripeCon](https://stripecon.eu) 👋
