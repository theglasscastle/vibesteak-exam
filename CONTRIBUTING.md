# Contributing questions

Thank you for helping make the exam harder. A good question is a real restaurant that a careful person can confirm, and that today's agents still get wrong.

**The one rule: answer keys never go through GitHub.** Not in a pull request, an issue, a comment, a commit message, a file name or an image name. A question whose answer has been posted in public is burned: we close it, and you are welcome to send a different one.

## What a question looks like

Every question asks for three fields: **restaurant name, street address, signature dish**. There are three kinds of input, plus one long format:

| Kind | Input | Asks |
|---|---|---|
| Link | A public post on a platform (Douyin, Xiaohongshu, Instagram, TikTok, X, Facebook, ...) | Which restaurant is this post about? |
| Photo | An original photo with GPS in its EXIF | Which restaurant was this photo taken at? |
| Location | Coordinates, a place hint and a cuisine | What is the best restaurant of that cuisine nearby? |
| Epic | One link that covers several restaurants | List every restaurant, three fields each |

Each prompt is written as **two lines with the same meaning: Chinese first, then English**. Use the wording below and change only the link, the file, the coordinates, the place hint or the cuisine.

Link:

```
这条链接里讲的是哪家店?给我店名、门牌地址和招牌菜。 <link>
Which restaurant does this link talk about? Give the name, street address and signature dish. <link>
```

Photo:

```
这张照片是在哪家店拍的?店名、门牌地址、招牌菜。 照片:<file>
Which restaurant was this photo taken at? Name, street address, signature dish. Photo: <file>
```

Location (four decimals; the place hint is a district and a street, in the local language):

```
我的位置:北纬 <lat> 东经 <lon>(<place hint>)。附近最好的<cuisine>是哪家?店名、门牌地址、招牌菜。
My location: <lat>, <lon> (<place hint>). What is the best <cuisine> restaurant nearby? Name, street address, signature dish.
```

For the western or southern hemisphere, write 西经 / 南纬 in the Chinese line and a negative number in the English line, as in the Starter paper.

Epic:

```
这条视频讲了几家店?把每一家的店名、门牌地址和招牌菜都列出来。 <link>
How many restaurants does this video cover? List the name, street address and signature dish of each one. <link>
```

## Difficulty

| Level | Meaning | Limit |
|---|---|---|
| ★ | Entry level. The name is in the post, or visible in the photo (storefront, menu, packaging). | 120 s |
| ★★★ | Hard. For photos: dishes only, no name visible, so the agent has to work from the GPS and the food. Links and locations where the answer takes real digging. | 120 s |
| Epic | One link, several restaurants, names perhaps only in the comments or the voice-over. 3 points per restaurant. | 10 min |

Some existing questions are marked ★★; new questions use ★, ★★★ or Epic.

Photo questions work best in pairs from the same restaurant: one photo with the name visible (★) and one with dishes only (★★★). A single photo is fine too.

## Requirements

**Photos**

- The original file as the camera saved it, with GPS in its EXIF. Not a screenshot, and not a copy that went through a chat app or an editor (those usually strip the location).
- No faces and no identifiable people.
- No blurring, masking or other editing. Pick a photo that needs none.
- You took it yourself, or you have the photographer's permission, and you agree to release it under CC BY 4.0 as part of the exam.
- Give it a neutral file name, such as `photo-1.jpg`. Never the restaurant's name.
- GitHub may remove location data from images pasted into issues and comments. Commit the original file in a pull request, or attach it to the issue as a `.zip`.

**Links**

- A public post on the platform itself. The platform's own share link is fine; other link shorteners and mirrors are not.
- About one restaurant (several for Epic) that exists and is open.

**Locations**

- A restaurant of that cuisine that is clearly the best choice within walking distance, and that a person can confirm.

**Every question**

- The answer is confirmable on at least two independent sources, such as a map listing plus the restaurant's own page or a review platform.

## How to send a question

1. **Pull request** (preferred, required for photos): add one file per question at `proposals/<your-handle>-<n>.md`, using the format of the papers in `questions/`:

   ```
   ## <kind> · <difficulty> · <platform> · <country>

   <Chinese line>
   <English line>
   ```

   Put a photo next to it as `proposals/<your-handle>-<n>.jpg`. Leave the question ID to us. Do not edit the files in `questions/` or `leaderboard/`: they mirror the live site.

   **Issue**: open a **New question** issue and fill in the template.

2. **Send the answer key privately** to truth@vibesteak.ai, or through the private form on vibesteak.ai once it is up. Put the PR or issue number in the subject. Include the three fields and your two sources.

3. **We check it.** Maintainers confirm the answer on two independent sources before it goes into the private answer key.

4. **We test it.** We run the question on the agents we test. It is accepted only if it stumps at least two of them: at least two agents fail to get full marks.

5. **It joins a paper.** Accepted questions are added in a later paper version with an ID from us, and the PR or issue is closed with a note.

## Credit and license

- Accepted questions are credited to the GitHub handle or the name you give in the PR or issue. Say "anonymous" if you prefer.
- Photo credit goes to the photographer you name.
- By contributing a question or photo, you release it under [CC BY 4.0](LICENSE-QUESTIONS). Code contributions are under the [MIT License](LICENSE).

## Other contributions

- **A broken question** (dead link, closed restaurant, unclear wording): open an issue. Describe the problem without posting the answer.
- **A wrong result on the leaderboard**: open a **Correction** issue or email corrections@vibesteak.ai.
- **Docs and templates**: pull requests are welcome.
