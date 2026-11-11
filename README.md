# Coptic Ask plugins: «اسأل البابا شنوده» and «اسأل آباء الكنيسة»

Two plugins for Claude and Codex that answer spiritual and Bible questions with clips of real recorded lectures and
sermons, the way our Android apps do: video and audio parts with exact time ranges, Bible references, Arabic captions,
and English subtitles and dub where available, plus links to open each answer on the web and in the app.

| Plugin | Answers from |
|---|---|
| [`ask-pope-shenouda`](plugins/ask-pope-shenouda) — Ask Pope Shenouda, اسأل البابا شنوده | the recorded lectures of Pope Shenouda III |
| [`ask-church-fathers`](plugins/ask-church-fathers) — Ask the Church Fathers, اسأل آباء الكنيسة | recorded sermons and lectures of Coptic Orthodox fathers and teachers |

## Install

Claude Code:

```
/plugin install ask-pope-shenouda --marketplace compujohnny/coptic-ask-plugins
/plugin install ask-church-fathers --marketplace compujohnny/coptic-ask-plugins
```

Codex:

```
codex plugin marketplace add compujohnny/coptic-ask-plugins
codex plugin add ask-pope-shenouda@coptic-ask
codex plugin add ask-church-fathers@coptic-ask
```

Any MCP client (Streamable HTTP, no sign-in): `https://copticask.jesox.com/pope/mcp` and
`https://copticask.jesox.com/fathers/mcp`.

## Bible reader (Ask the Church Fathers)

Ask to read any chapter ("read me the chapter in John about Lazarus", «اقرأ لي المزمور ٢٣»): the plugin opens it in
the CopticBible reader. In Claude and ChatGPT it is a card inside the chat; elsewhere a link to the same reader page.
Read the Arabic text, listen to the chapter with the verse being read highlighted, tap any verse to see and hear the
fathers' recorded commentary on it, and move to any chapter or book.

## Readings across the Bible

Ask about a subject or a question ("psalms about love", «آيات عن الرجاء»): the plugin gathers passages from across the
Bible, and the reader shows and reads them one after another (only those verses), with the fathers' commentary on any
verse and a list to jump between passages.

## How answers are shown

Every answer follows the rendering contract `coptic-ask/1.0`
([RENDERING.md](plugins/ask-pope-shenouda/skills/ask-pope-shenouda/references/RENDERING.md)): the title, "listen to the
whole answer", numbered part cards (heading, speaker and lecture, references, summary, time range, play link), then the
web, app and Google Play links. Arabic stays right to left. Nothing is generated: every part is the speaker's own words.

## Privacy and terms

- Ask Pope Shenouda: [privacy](https://compujohnny.com/pope-shenouda/privacy/) · [terms](https://compujohnny.com/pope-shenouda/terms/)
- Ask the Church Fathers: [privacy](https://compujohnny.com/ask-the-church-fathers/privacy/) · [terms](https://compujohnny.com/ask-the-church-fathers/terms/)

Support: [open an issue](https://github.com/compujohnny/coptic-ask-plugins/issues).
