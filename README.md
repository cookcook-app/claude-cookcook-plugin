# CookCook for Claude

CookCook is a catalogue of printed cookbooks and the recipes inside them. This
plugin connects Claude to it, so you can cook from the books on your own
shelf instead of from the internet.

Ask which of your cookbooks has a recipe for pumpkin soup, what is in a book's
index before you buy it, or what you could make tonight from the leeks in the
fridge and the books you own. CookCook answers with the book, the page and the
ingredients, and links the recipe on cookcook.app.

Two things start from a photograph. Show Claude a picture of your bookshelf and
the books it can read land on your CookCook shelf. Photograph a recipe page
from a book you own and Claude transcribes it into your own captured recipe,
with its ingredients and method, ready for your grocery list.

Connecting your CookCook account from the plugin's Connectors tab adds your
library, your saved recipes, your collections and your grocery list. Sign-in
goes through CookCook's own OAuth; the plugin holds no keys or secrets.

For a catalogue recipe CookCook knows the title, the page and the ingredient
names — not the method or the quantities. Those stay in the book, which is the
point: the book is still the cookbook.

## Installing

In Claude Code, add this repository as a marketplace and install the plugin:

```bash
claude plugin marketplace add cookcook-app/claude-cookcook-plugin
```

```bash
claude plugin install cookcook@cookcook
```

On claude.ai or in the Claude desktop app: Customize → Plugins → Add → Add
marketplace, and paste this repository's URL,
`https://github.com/cookcook-app/claude-cookcook-plugin`.

Then connect your CookCook account from the plugin's Connectors tab (in Claude
Code: `/mcp`). Without a CookCook account you can still add the public
catalogue as a plain connector: `https://www.cookcook.app/api/mcp`.

## What is in this repository

- `.claude-plugin/plugin.json`: the plugin's manifest.
- `.claude-plugin/marketplace.json`: makes this repository a marketplace with
  one plugin in it.
- `.mcp.json`: the CookCook connector, `https://www.cookcook.app/api/mcp/me`.
- `skills/`: when to use which CookCook tool, how to plan a menu from your
  cookbooks, how to read a shelf photo, and how to capture a recipe from a
  photographed page.

- Website: https://www.cookcook.app
- Privacy: https://www.cookcook.app/privacy
- Questions: support@cookcook.app
