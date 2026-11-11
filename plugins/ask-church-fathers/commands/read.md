---
description: Ask the Church Fathers (اسأل آباء الكنيسة) — open a Bible chapter in the CopticBible reader (read, listen, commentary)
argument-hint: <a chapter, a reference, or what the passage is about>
---

Open the Bible passage(s) the user asks for in the CopticBible reader with the `ask-church-fathers` MCP tools:
0. If it asks for a SUBJECT or a QUESTION (e.g. «مزامير عن المحبة», "verses about hope", "what does the Bible say
   about forgiveness"), make a reading: `open_reading(title, passages)` with enough passages from across the Bible to cover
   the subject fully (no fixed number, at most 30), ordered by spiritual importance, the most central first, not Bible
   order. For a STORY (a person's life, a story, an event: «ما هي قصة داود؟») order the passages as it happened, the
   key episodes from beginning to end, events told twice only once, psalms placed at their moment, each note a short
   caption of the episode
   ({book, chapter, from, to, note}; several psalms, prophets, Gospels, epistles), chosen from your knowledge and checked
   with `find_passage` when unsure. The reader reads them one after another. Then stop: steps 1-2 are for one chapter.
1. If it names a book and chapter (or a reference such as «يوحنا ١١: ٣٥», "Psalm 23"), call `open_chapter(book, chapter,
   verse?)` directly. If you know which chapter a description means (the raising of Lazarus -> John 11), use it.
2. Otherwise call `find_passage` with Arabic words for the topic (translate English topics to Arabic, e.g. a psalm about
   prayer -> «صلاتي», «اسمع يا رب صلاتي», with book "PSA"), pick the best hit, and call `open_chapter` with it.
3. Show the returned markdown as is (hosts with cards show the reader inside the chat). Don't retype the chapter's text.
   Opening chapters is free; never call `ask` for a reading request.

$ARGUMENTS
