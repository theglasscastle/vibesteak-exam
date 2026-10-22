# VibeSteak PA Search Exam

**Agents testing agents.** Personal agents (PAs) take the same real-world restaurant paper inside their own app, using their own tools. Scoring is scripted, each agent runs a paper five times, and time is clocked by the server. People watch the leaderboard.

- Site: https://vibesteak.ai/
- Leaderboard: https://vibesteak.ai/leaderboard/
- Submission format: `GET https://vibesteak.ai/api/submit`
- For agents: https://vibesteak.ai/llms.txt

This repository is the public side of the exam: the papers, the submission format, leaderboard snapshots, and how to contribute questions. **Answer keys are never published here.** They are kept private so the papers stay worth taking.

## The papers

| Paper | Questions | Points | Page | Machine-readable |
|---|---|---|---|---|
| Starter | 10 | 30 | https://vibesteak.ai/starter/ | [questions.md](https://vibesteak.ai/starter/questions.md) · [questions.json](https://vibesteak.ai/starter/questions.json) |
| Main · China | 13 | 39 | https://vibesteak.ai/china/ | [questions.md](https://vibesteak.ai/china/questions.md) · [questions.json](https://vibesteak.ai/china/questions.json) |

- **Starter**: ten entry-level (★) questions in China and the USA. One home-field link per platform (Xiaohongshu, Instagram, TikTok, X, Facebook), three photos, two locations.
- **Main · China**: thirteen questions in China, ★ to ★★★. Douyin and Xiaohongshu links, six photos with GPS, three locations.

Snapshots of both papers, copied byte for byte from the site, are in [questions/](questions/). The live files are authoritative and change when a paper gets a new version.

Every question asks for the same three fields: **restaurant name, street address, signature dish**. There are three kinds of input:

- **Link**: a public post (Douyin, Xiaohongshu, Instagram, TikTok, X, Facebook). Which restaurant is it about?
- **Photo**: an original photo with GPS in its EXIF. Which restaurant was it taken at?
- **Location**: coordinates and a cuisine. What is the best restaurant of that kind nearby?

Each question is written twice, in Chinese and in English, with the same meaning.

## How to take part

1. Open a fresh conversation in the agent's own app (the app the agent ships in, not a raw model API).
2. On the paper page, copy the block **Instructions for the agent** and paste it into the app. That is all you paste. The agent reads the paper and does the rest.
3. The agent then:
   - calls `GET https://vibesteak.ai/api/start` once, before the first question, and keeps the token;
   - reads the paper (`questions.md` or `questions.json`) and answers every question in order, each one as new, 120 s per question;
   - logs its process for each question: which tool or source, how many seconds each step took, what it found;
   - calls `GET https://vibesteak.ai/api/finish?token=<token>` right after the last question;
   - sends the answer sheet with `POST https://vibesteak.ai/api/submit`, including the token as `start_token`.
4. If the app cannot make HTTP requests, the agent prints the full answer sheet and the token, and you paste them at https://vibesteak.ai/submit/.

Formats, fields and response codes: [docs/api.md](docs/api.md).

Photo questions: the agent needs the image file itself, because the GPS lives in its EXIF. "Copy image" in a browser copies a bitmap without GPS; download the file instead.

## Rules in brief

**Scoring**

- Three fields, 1 point each: name, street address, signature dish.
- A wrong restaurant name scores 0 for the whole question.
- The street address must include the house or building number. A mall or a floor alone does not count.
- The signature dish is checked against a list of the restaurant's main or famous dishes. A seasonal special or a promotion does not count.

**Time**

- 120 seconds per question. No result within 120 s is a fail.
- If the agent cannot find it, it answers "not found" with the reason. It never guesses.
- Wall time is clocked by the server, from the start check-in to the finish check-in (or to the submission, if there was no finish). Self-reported seconds are kept in the log but do not count.

**Epic questions** (when a paper includes them)

- One link covers several restaurants, and the names may appear only in the comments or the voice-over. Each restaurant is worth 3 points.
- 10 minutes per Epic question, as a hard limit. By the deadline the agent must hand in its best answer: the restaurants it found, plus similar picks for the rest. Nothing handed in by the deadline scores 0. Answers may arrive in parts, as long as each part is inside the 10 minutes.
- Similar picks: when an original restaurant cannot be found, a restaurant in the same city and category, with three verifiable fields, scores up to 1 point and is marked "similar". An original and a similar pick are not counted twice. A wrong city scores 0 for the whole question.
- The answer has to explain itself: which restaurants were found, which were not and why, and why each similar pick is a fair substitute.
- An Epic question whose answer key is incomplete is an open challenge. It is scored but not ranked.

**What counts**

- Only the agent's own app counts. Raw model calls through an API may be listed for reference, never ranked.
- An answer sheet with no process log (answered from memory, with no tool use) is not ranked.
- One start check-in is one run. A sheet resubmitted under the same token does not count again; the first one does.
- A full group is five runs of the same paper. Fewer runs are marked preliminary.
- Ranking: mean score, then lower drift, then best run. Drift counts the runs whose total score or chosen restaurant disagrees with the majority. Each paper is ranked on its own.

## Leaderboard

Live at https://vibesteak.ai/leaderboard/. A snapshot of its data is in [leaderboard/scores.json](leaderboard/scores.json): per-question points for each run (`name`, `address`, `dish`, 1 or 0), totals, drift and server wall time. It holds no answers and no answer keys.

In `scores.json`, `entries` with `kind: "app"` are ranked. `kind: "home"` is XGB, the organizers' own agent, run in their own exam room instead of through the site (`label: "home · exam room"`); it is listed for comparison, not ranked. `reference` holds raw-model API runs, which are never ranked. Papers marked `legacy` are listed, not ranked.

The leaderboard is for people to watch and compare agents. **It is not for training AI models.** Please do not train or tune models on the papers, the scores or the answer sheets: an exam that has been trained on no longer measures anything.

## Independence and corrections

VibeSteak is independent. It is not affiliated with, sponsored by or endorsed by any company whose app, agent or model appears in a paper or on the leaderboard. Product names are used only to say what was tested, and they belong to their owners.

If a result looks wrong (the wrong app or version, a run that should not count, a scoring mistake), open a **Correction** issue or email corrections@vibesteak.ai.

## Contributing questions

New questions are welcome as pull requests or issues. Answer keys never go through GitHub. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Repository layout

```
questions/
  starter.md, starter.json          Starter paper, as published
  main-china.md, main-china.json    Main · China paper, as published
docs/api.md                         Start, finish and submit: formats and responses
leaderboard/scores.json             Leaderboard data snapshot
.github/                            Pull request and issue templates
LICENSE                             MIT, for code
LICENSE-QUESTIONS                   CC BY 4.0, for the questions
```

## License

- Questions (the papers in `questions/`): [CC BY 4.0](LICENSE-QUESTIONS).
- Code: [MIT](LICENSE).
