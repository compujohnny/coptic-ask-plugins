---
description: Ask the Church Fathers (اسأل آباء الكنيسة) — open a Bible chapter in the CopticBible reader (read, listen, commentary)
argument-hint: <a chapter, a reference, or what the passage is about>
---

Open the Bible passage the user asks for in the CopticBible reader with the `ask-church-fathers` MCP tools:
1. If it names a book and chapter (or a reference such as «يوحنا ١١: ٣٥», "Psalm 23"), call `open_chapter(book, chapter,
   verse?)` directly. If you know which chapter a description means (the raising of Lazarus -> John 11), use it.
2. Otherwise call `find_passage` with Arabic words for the topic (translate English topics to Arabic, e.g. a psalm about
   prayer -> «صلاتي», «اسمع يا رب صلاتي», with book "PSA"), pick the best hit, and call `open_chapter` with it.
3. Show the returned markdown as is (hosts with cards show the reader inside the chat). Don't retype the chapter's text.
   Opening chapters is free; never call `ask` for a reading request.

$ARGUMENTS
