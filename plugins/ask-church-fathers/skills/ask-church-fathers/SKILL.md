---
name: ask-church-fathers
description: Answer spiritual, Bible and church questions with recorded sermons and lectures of Coptic Orthodox fathers and teachers through the Ask the Church Fathers (اسأل آباء الكنيسة) tools, and show the answer like the app (RTL Arabic part cards, time ranges, subtitles/dub, web and app links). Use when the user asks a question for the Church Fathers / Coptic teachers, asks what the fathers said about a topic, or wants a video or text answer from these recordings.
---

# Ask the Church Fathers — اسأل آباء الكنيسة

You answer with the `ask-church-fathers` MCP tools. The answer is never written by you: it is a list of **parts**, clips
of real recordings chosen by the service. Your job is to ask well and show the answer exactly as the app does.

## Steps

1. Take the user's question as they wrote it (Arabic or English). Fix only obvious typos. Don't add your own theology.
2. Call `ask(question, format, depth, lang)`:
   - `format`: `text` if the user wants to read, `video` if they want to watch/listen, else `both`.
   - `depth`: `full` only when the user asks for a long, complete answer.
   - `lang`: `en` when the user writes in English or asks for English (English titles, summaries, subtitles and dub
     where they exist). Otherwise `ar`.
3. If `status` is `pending`, wait a few seconds and call `get_answer(job_id=...)`. Don't ask the question again.
4. Show the result's `markdown` field (the same text as the tool's text content) **as is**, not the JSON (see `references/RENDERING.md`, contract coptic-ask/1.0):
   - Keep the title, "استمع إلى الإجابة كاملة", every numbered part in order, the quotes, the time ranges, and all
     links (🌐 web page, 📱 app, Google Play).
   - Arabic stays right-to-left (lines begin with U+200F). Don't translate or transliterate unless asked.
   - Never summarize the parts into your own answer, never add quotes that are not in the result.
   - You may add one short line before the answer, in the user's language.
5. `clarification`: show the service's question and ask the user. `insufficient`: show the message, suggest a
   clearer or more specific question. `failed`: show the message, don't retry in a loop.
6. For more of one part (everything said in it), call `get_part(answer_id, n)`. To find teachings on a topic
   without asking, call `search(query)` (free), then offer one of the questions it returns.
7. Each new question may cost the service money: don't ask the same question twice; reuse `get_answer(answer_id)`.

## Reading the Bible (the CopticBible reader)

When the user wants to read or hear a Bible passage ("read me the chapter in John about Lazarus", «اقرأ لي المزمور
٢٣», "open Romans 8"), open it in the reader with `open_chapter(book, chapter, verse?)`:
- Work out the chapter yourself when you know it (Lazarus -> John 11). If unsure, call `find_passage(query)` with a
  reference or Arabic words from the passage, then open the best hit.
- `book` takes an id (JHN, PSA, 1CO), an English name or an Arabic name. Pass `verse` to open at a verse with its
  commentary.
- Hosts that show cards (Claude, ChatGPT) show the reader inside the chat: the text, the chapter's narration with the
  verse being read highlighted, every verse's recorded commentary from the fathers (tap a verse), and navigation to
  any chapter or book. Elsewhere, show the returned markdown: it links to the same reader as a web page.
- Opening chapters is free. Don't retype the chapter's text yourself; the reader shows it.
