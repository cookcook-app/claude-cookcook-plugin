---
name: shelf-photo
description: Turn a photo of a bookshelf into cookbooks on the reader's CookCook shelf. Use whenever someone attaches or describes a picture of their bookshelf, a stack or a pile of cookbooks, or asks to add their books, scan their shelf, catalogue their collection or get their cookbooks into CookCook from a photo. Read the spines yourself, match them with match_shelf_books, and add them with add_books_to_library only after the reader confirms.
---

# A photo of a bookshelf

The reader shows a shelf; the books end up on their CookCook shelf. You do the
reading — CookCook's tools take text, never the image.

## 1. Read the spines yourself

Look at the photo and write down, for each book you can see, the title and the
author if the spine shows one. Work left to right so the reader can follow
you.

- Read only what is legible. A spine that is turned away, cut off, blurred or
  hidden behind another book is **not** a title: leave it out, and say how
  many you could not read.
- Never guess, complete or "correct" a title from what you know of cookbooks.
  Half a word is half a word; pass what you actually read, or nothing.
- Say so plainly when the photo holds no books, or when nothing is legible,
  and ask for a closer or better-lit picture instead of guessing.
- Books that are not cookbooks belong in the list too if the reader asked for
  their whole shelf — CookCook will simply not match them.

## 2. Match them against the catalogue

Call `match_shelf_books` with the titles you read, each with its author where
you have one. One call for the whole shelf (up to 40 books), in the order you
read them. It writes nothing, so it is always safe to call.

Each result comes back with a `confidence`. **Anything below 0.7 is a question,
not an answer**: it carries its runners-up as `alternatives`, so put the match
and its alternatives to the reader and let them pick, rather than choosing the
top one yourself. Results also say whether the book is already `in_library`.

## 3. Show the reader before you add anything

Report back in three groups, so nothing is added behind their back:

- **Found** — confident matches, by title, author and year, with the CookCook
  link and the cover where you can show images. Say which are already on their
  shelf, so they are not re-added.
- **Not sure** — everything under 0.7 confidence, each with its alternatives,
  asked as a question. A different edition, a different author or a translated
  title belongs here, not above.
- **Not in the catalogue** — titles you read that matched nothing. Say that
  adding them may create a new catalogue entry from the ISBN, if that is what
  the tool reports.
- **Could not read** — the spines you skipped, counted, not invented.

A book CookCook does not have is still a book on their shelf: say that they
can photograph a recipe page from it and capture it anyway (the
`capture-recipe` skill), with the book added by ISBN and attached afterwards.

Then ask whether to add them, and say exactly which. Offer to drop the ones
they do not own or do not want.

## 4. Add them

On a clear yes, call `add_books_to_library` with the books they confirmed.
Report what landed on their shelf and what did not, and link the shelf. If
they picked a subset, add that subset and nothing more.

Never call `add_books_to_library` on the strength of a photo alone: the
confirmation step is the whole point. A reader who says "yes, add them all" up
front has confirmed; still show the list first, so they can see what "all"
turned out to mean.
