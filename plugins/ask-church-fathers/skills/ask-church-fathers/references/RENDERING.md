# Rendering contract: coptic-ask/1.0

How an agent shows an answer from «اسأل البابا شنوده» (Ask Pope Shenouda) or «اسأل آباء الكنيسة» (Ask the Church
Fathers) so it matches the apps. The `ask`, `get_answer` and `get_part` tools return:

- `content[0].text`: the answer already rendered in markdown by this contract. **Show it as is.**
- `structuredContent`: the same answer as data (fields below), for agents that build their own view. Its first field,
  `markdown`, is the same rendered text: clients that pass only structured content to the model show that field.

## Rules

1. **The parts are the answer.** Every part is a clip of a real recording, chosen by the service. Never summarize,
   merge, reorder, re-title or add teaching of your own. You may add one short line before the answer (for example,
   "Here is the answer from Pope Shenouda's lectures:"), and nothing after it except the user's follow-up.
2. **Order (as in the app):**
   1. The title, as a heading.
   2. "▶️ استمع إلى الإجابة كاملة" (listen to the whole answer), with the part count and the total minutes.
   3. The numbered parts. Each part card has the number and heading (bold), then the teacher and lecture line, then
      the Bible references as chips (`متى ٩: ٣٦`), then the summary, then the quote (text mode), then
      "▶️ استمع · m:ss", the time range, and the subtitle/dub tags.
   4. A rule, then the links: 🌐 the web page, 📱 the app (Android), Google Play.
3. **Arabic is right-to-left.** Lines start with U+200F (RLM) so they align right in mixed-direction views. Keep it.
   Numbers in Arabic text use Arabic-Indic digits (١٢٣). Time ranges and links stay left-to-right (wrapped in U+200E).
   Don't transliterate or translate the Arabic unless the user asks. With `lang: "en"`, English titles, summaries and
   subtitles appear next to the Arabic where they exist. Show both.
4. **Quotes** are the speaker's own words from the captions, inside «…». Put them in a block quote. Never put
   words in quotes that are not in `transcript_ar` / `transcript_en`.
5. **Links:** keep every link. `links.web` opens this same answer on our website, with the app's player. `links.app` (https) opens
   the Android app at this answer (Google Play when it is missing; the web page on other devices). `links.play_store` is the Play Store page.
   Per part, `watch_url` opens the web player at that part, and `play_url` is the direct media for players that
   can embed it (it honours `#t=start,end`).
6. **Statuses:** `pending` means say it's being prepared and call `get_answer(job_id=…)` after a few seconds.
   `clarification` means show the service's question and ask the user. `insufficient` means show the message and
   suggest rewording. `failed` means show the message and don't retry in a loop.
7. **Cost:** each new question may cost the service money. Don't ask the same question twice: use `get_answer(answer_id)`.

## Structured answer (`structuredContent`)

```
markdown     the rendered answer (same as content[0].text)
contract     "coptic-ask/1.0"
app          {key: "pope"|"fathers", name, name_en}
status       answerable | clarification | insufficient | pending | failed
question, title, answer_id (24 hex), depth (short|full), lang, cached
total_seconds, play_all_url
links        {web, site, app, app_intent, app_uri, play_store}
parts[]      {n, id, heading, title, summary, teacher, teacher_name, source_line, library (commentary|sermon), kind,
              refs[], vid, start, end, seconds, time_range "m:ss–m:ss",
              media {kind: video|audio|hls, has_video}, watch_url, play_url,
              subtitles {ar: bool, en: bool}, dub_en: bool,
              en? {title, summary}, transcript_ar, transcript_en?}
```

Fields are only ever added in 1.x. A breaking change becomes 2.0.

## Example (text mode, shortened)

```
## ‏كيف ننتصر على الخطية؟

‏▶️ **[استمع إلى الإجابة كاملة](https://…/pope/a/3f…?p=1&all=1)** — ٣ مقاطع من محاضرات قداسة البابا · ٦ دقائق

### ‏١. الخطية تبدأ بفكر
‏من محاضرة: حروب الأفكار · ١٢/٣/١٩٩٨
‏`يعقوب ١: ١٤`

‏يشرح قداسة البابا كيف تبدأ الخطية بفكر يُقبَل ثم يتحوّل إلى شهوة ففعل.

> ‏«الخطية لا تبدأ بالفعل، إنما تبدأ بفكرة …»

‏▶️ [استمع · ٢:١٠](https://…/pope/a/3f…?p=1) — من ‎14:02–16:12‎ · ترجمة عربية · English subtitles
…
---
‏🌐 [اعرض الإجابة على موقع اسأل البابا شنوده](https://…/pope/a/3f…) · 📱 [افتح في التطبيق (أندرويد)](intent://…) · [حمّل التطبيق من Google Play](https://play.google.com/…)
```

In video mode, each part also gets a direct media link next to the player link. Agents that can show HTML or
video players (MCP Apps hosts) may use `watch_url` in an embedded view. Every other agent shows the markdown.
