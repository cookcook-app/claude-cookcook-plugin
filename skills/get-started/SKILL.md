---
name: get-started
description: How to answer with CookCook — the catalogue of cookbooks and the recipes printed in them, plus the reader's own library. Use whenever someone asks which cookbook has a recipe for something, what is in a cookbook's index, what they could cook from the books they own, or asks about their CookCook library, saved recipes, collections or grocery list. Also covers what CookCook does and does not know about a recipe.
---

# CookCook

CookCook is a catalogue of printed cookbooks and the recipes in them: every
recipe's title, the page it is on, and the ingredient names it uses. It is a
way to cook from the books someone already owns, not a recipe website.

## What CookCook knows, and what it does not

- For a catalogue recipe CookCook has the **title, the book, the page numbers
  and the ingredient names** — not the method and not the quantities. Those
  are in the book. Say which book and which page, and leave the cooking to the
  page.
- Never fill the gap by writing a method or quantities of your own for a
  catalogue recipe. If the reader wants the recipe itself, point them at the
  page, or at `get_my_recipe`, which gives their own copy when they captured
  it or hold the book as an ebook.
- Always link the CookCook URL of every book and recipe you name, and show the
  cover (`cover_image_url`) beside a book where you can display images.

## Finding recipes and books

- "Which cookbook has a recipe for pumpkin soup?" → `search_recipes` with the
  dish or the ingredient. Answer with each recipe's title, its book and page.
- "What's in *Ottolenghi Comfort*?" → `search_books` to find the book, then
  `get_book` for its details and its recipe index.
- `get_recipe` gives one recipe's ingredient names and the book it is in.

## The reader's own shelf

These tools work on the reader's CookCook account, which they connect once
from the plugin's Connectors tab.

- "What can I cook tonight?" / "What can I make with the leeks in my fridge?"
  → `search_my_books`, which searches only the recipes in the books they own.
  Prefer it over `search_recipes` whenever they ask what *they* could cook.
- `my_books`, `my_saved_recipes`, `my_collections` and `get_collection` read
  their library; `get_my_recipe` reads their own copy of a recipe, with the
  method when they captured it or hold the book as an ebook.
- `get_grocery_list` and `add_to_grocery_list` work on the grocery list. Add
  exactly what they asked for, nothing else.
- `save_recipe`, `like_recipe`, `rate_recipe`, `mark_cooked`, `log_tasting`,
  `add_to_my_books`, `wishlist_book`, `like_book`, `rate_book`,
  `comment_on_book`, `create_collection`, `add_to_collection` and
  `remove_from_collection` change their library, as the buttons on CookCook
  do. Use them only when asked, and never invent a rating, a note or a
  comment on their behalf.

## Photographs

Two things start from a photo, and each has a skill of its own:

- A photo of a **bookshelf** → read the spines and add the books (the
  `shelf-photo` skill).
- A photo of a **recipe page** → transcribe it into their own captured recipe
  (the `capture-recipe` skill). Ask which book it came from; a book CookCook
  does not have can be added by ISBN and attached afterwards with
  `link_recipe_to_book`.
