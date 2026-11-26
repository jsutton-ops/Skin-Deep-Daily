# Skin Deep Daily: academic year version

Skin Deep Daily is a daily knowledge check on skin structure for Level 2 Beauty learners (City & Guilds 3003). It runs on weekdays from September to May.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The game page. |
| `questions.js` | The question bank (201 questions) and settings. |
| `README.md` | This guide. |

Keep `index.html` and `questions.js` in the same folder. The page shows "The questions did not load" if `questions.js` is missing.

## How the game works

- **A new set at 4:00pm UK time, Monday to Friday.** The switch-over follows UK time, including British Summer Time.
- **Friday's set stays open over the weekend.** The next new set opens at 4:00pm on Monday.
- **September to May only.** A new set opens on the first weekday of September at 4:00pm. The last set of the year closes on the first weekday of June at 4:00pm. From June to August, learners see a summer break screen with their knowledge gaps to revise.
- **Five class questions each day.** All learners get the same five on the same day, so you can go through them together in class. Each question comes up about 3 to 5 times across the year.
- **Feedback on every answer.** A correct answer shows an explanation. A wrong answer shows the right answer, an explanation and a "Further study" box with specific revision advice.
- **A results screen.** This shows the score, a study plan built from any wrong answers, a review of every question, a count of knowledge gaps and topic strength bars.

### Spaced repeats of knowledge gaps

A question a learner gets wrong becomes a **knowledge gap** for that learner only.

1. It is added to their **next** set as a review question. Up to 3 review questions come before the 5 class questions.
2. If they answer it correctly, it comes back **3 sets later**.
3. If they answer it correctly again, it comes back **7 sets later**.
4. A third correct answer in a row **closes** the gap.
5. A wrong answer at any stage starts the steps again from step 1.

The oldest gaps are shown first. If more than 3 are due on the same day, the rest wait for the following sets.

### Where progress is saved

Progress is saved in the learner's browser on their device (`localStorage`). There are no logins and no data is sent anywhere. This means:

- If a learner uses a different device or browser, they start again on that one.
- Private or incognito windows don't keep progress after they are closed.
- Clearing browser data resets their progress.
- **Reset my progress** at the bottom of the page clears that learner's progress on that device.

## Hosting on GitHub Pages

1. Add `index.html` and `questions.js` to a repository, either in its own folder or in the root.
2. In the repository, open **Settings > Pages**. Choose **Deploy from a branch**, then pick your branch and folder.
3. After a minute or two the game will be live, for example at `https://<your-username>.github.io/<repo>/` or `.../<repo>/<folder>/`.

## Embedding in SharePoint

1. Edit the SharePoint page and add an **Embed** web part.
2. Paste an iframe that points to your GitHub Pages address:

   ```html
   <iframe src="https://<your-username>.github.io/<repo>/" width="100%" height="900" style="border:0" title="Skin Deep Daily"></iframe>
   ```

3. If SharePoint says embedding from that site isn't allowed, a site admin needs to add `github.io` under **Site settings > HTML Field Security**.

The page adapts to the width of the frame and works on phones.

## Editing questions

Open `questions.js` in any text editor, such as Notepad or VS Code. Each question looks like this:

```js
Q(`Dermis`, `Which fibres give the skin its strength?`,
 [`Collagen`, `Elastin`, `Keratin`, `Melanin`],
 `Explanation shown after every answer.`,
 `Further-study advice shown when the answer is wrong.`),
```

- **The first option is always the correct answer.** The game shuffles the options on screen.
- Each question needs exactly **4 options**.
- Text goes between backticks (`` ` ``), so apostrophes and quotation marks are fine. Don't use a backtick inside the text.
- End each question with `),` and put the next one underneath.
- **Add new questions at the end of the list only.** Don't delete or reorder questions, because each learner's knowledge gaps are tracked by a question's position in the list. To fix or retire a question, change its wording instead.
- Adding questions changes which questions appear on which day from then on. It's best to do this over the summer break.

**Topics in use:** Epidermis, Dermis, Subcutaneous, Appendages, Hair & nails, Functions, Skin types, Conditions, Skin health. Use one of these names exactly. Each one has its own topic strength bar, and the skin diagram lights up the matching layer.

After editing, open `index.html` in your browser to check it still loads. If you see "The questions did not load", look for a missing backtick, bracket or comma near your change.

## Settings

The settings are at the top of `questions.js`:

```js
window.SKIN_CONFIG = {
  reviewPerDay: 3,
  closedDates: [
    ['2026-12-21', '2027-01-01'],
    ['2027-02-15', '2027-02-19'],
  ]
};
```

- **`reviewPerDay`** is the most review questions added to a learner's set each day. The default is 3.
- **`closedDates`** lists college holidays when no new set opens. Learners see a holiday break screen instead.
  - Each entry is `['first day', 'last day']` in `YYYY-MM-DD` format.
  - For a single day, use the same date twice.
  - You don't need to list weekends or June to August.
  - The list is empty to start with. Add your college's term dates each year.
  - Closed days don't break a learner's streak.

## Original version

The first version, `skin-deep-daily.html`, is a single file with 67 questions. It gives 5 questions every day of the year with no review questions. It still works on its own and can be hosted the same way.
