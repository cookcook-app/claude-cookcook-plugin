---
name: capture-recipe
description: Turn a photo of a recipe page from a cookbook into the reader's own captured recipe on CookCook, and attach it to the book it came from. Use whenever someone photographs or scans a page of a cookbook, asks to capture, save, transcribe or digitise a recipe out of a book they own, or mentions cooking something from one of their books and wanting it in CookCook with its ingredients and method. Transcribe the page yourself exactly as printed, ask which book it is from, show it back, and call capture_recipe only after the reader confirms. Never save a guess or a placeholder for a line you could not read: ask for another photo or have the reader read it out. A book CookCook does not have is no reason not to capture.
---

# A photo of a recipe page

The reader photographs a page of a cookbook; it becomes their own captured
recipe on CookCook, with the ingredients and the method. You do the reading —
CookCook's tools take text, never the image.

Offer this whenever someone mentions cooking from a book they own and the
recipe is not already in their library: "photograph the page and I'll put it
in your CookCook."

## 1. Transcribe the page, exactly as printed

Write out:

- the **title**, as printed;
- the **page number**, from the page itself — the folio, not a guess;
- the **ingredient lines**, one per line, word for word as printed, keeping
  the book's own amounts, units and order ("2 el olijfolie", "a knob of
  butter"). Do not convert, round, tidy or translate them;
- the **method**, step by step, in the book's words.

Rules that matter more than completeness:

- **Never invent a quantity, an ingredient, a step, a page number, a title or
  an ISBN.** No filling in from your own knowledge of the dish, however
  obvious the missing step seems, and no "about 200 g" where the page is
  blurred.
- **Never save a placeholder either** — no "[unreadable]", no "???", no empty
  line standing in for one you could not read. Everything in `ingredients` and
  `instructions` is saved as the recipe and run through CookCook's ingredient
  and instruction parsers, so a marker becomes a junk ingredient line on the
  reader's own sheet, and can follow them onto a grocery list.
- The reader is standing next to the book, which is a better source than a
  marker: when a line will not come out of the photo, **ask for another photo
  of that part, or ask them to read it out or type it**. Call `capture_recipe`
  only once every line is something you read or they supplied.
- If they would rather not, save nothing. A recipe with holes in it is worse
  than no recipe, because it looks finished.
- If the recipe runs onto another page, say so and ask for the rest before
  capturing — a half recipe is worse than none.
- Keep the book's language. Do not translate a Dutch recipe into English
  unless the reader asks, and then capture the original and note the
  translation separately.

## 2. Ask which book it came from

Settle the book, do not assume it. If the photo does not make it plain — a
running head, a chapter title — **ask the reader which book the recipe is
from**.

- Look on their own shelf first: `my_books`, or `search_my_books` for the
  recipe's title. The book is usually already there.
- When CookCook's index already has this recipe, pass its `recipe_id` rather
  than the book's `isbn`: that attaches the capture to the book's own index
  entry, where the ISBN alone only names the book. `search_my_books` and
  `get_book` are where those ids come from.
- Otherwise `search_books` against the catalogue, and show them the match to
  confirm rather than picking one yourself. Two editions of the same book are
  two different books.
- If the book is not in CookCook at all, say so plainly. That is not a reason
  to stop: capture the recipe anyway so the work is not lost, then offer to
  add the book — the ISBN from its barcode, or a photo of the cover and the
  title page — with `add_books_to_library`, and attach the capture afterwards
  with `link_recipe_to_book` (the capture's id, plus the book's `isbn` or,
  better, the `recipe_id` of its index entry).
- A capture with no book attached is fine and can be attached later. A capture
  attached to the wrong book is not.

## 3. Show it back

Give the reader the whole transcription — title, book, page, ingredient lines,
method — and ask them to check it. This is the moment to catch a misread
amount, so do not shorten it to a summary. If anything is still missing, this
is the moment to get it from them, not to capture around it.

## 4. Capture it

On a clear yes, call `capture_recipe` with the transcription as confirmed —
the title and page as printed, the ingredient lines one per line, the method
one step per line — and the book when it is settled, as `recipe_id` where the
index has the recipe, otherwise `isbn`, and neither when CookCook has no such
book. It becomes **their own pending capture**, visible
to them, not a public catalogue recipe; say so, and link it.

Afterwards you can offer the ordinary things: attach the book with
`link_recipe_to_book` if it was added later, add the ingredients to their
grocery list (`add_to_grocery_list`), save it (`save_recipe`), or log a
tasting once they have cooked it (`log_tasting`).

## What not to capture

- A recipe from a website, a magazine clipping or a screenshot of someone
  else's page: this is for the books the reader has in their hands.
- A page from a book they say is not theirs. Ask first.
