---
name: add-clip
description: Add one of Tyler's published stories to the Clips section of the personal site (index.html) from a link, then push so it goes live. Use when Tyler runs /add-clip with a story URL or asks to add a clip or story to the site.
argument-hint: <story URL>
---

# add-clip

Add a published story to the **Clips** section of `index.html`, then push so the live site updates.

The story link is: $ARGUMENTS

If no link was given, ask Tyler for one and stop.

## 1. Open the link and read the story details

Open the URL with whatever web-reading tool this session has (WebFetch, or the `web-fetch` agent). Ask it for:

- the **headline exactly as published**, character for character
- the **outlet** (publication name)
- the **publication date**

Use the headline shown on the article page itself (the `<h1>`). If the browser-tab title or social preview text is different, ignore it.

**Do not guess.** If the page can't be opened (paywall, login, error, blocked, timeout), or any of the three details is unclear or missing, stop. Tell Tyler what you couldn't get and ask him for the headline, outlet and date. Then continue with what he gives you, using it exactly as written.

## 2. Headline rules (strict)

- Copy the headline **exactly**: same words, capitalization, punctuation and curly quotes (‘ ’ “ ”).
- **Never** rewrite, shorten, summarize, retitle or "fix" it.
- The only change allowed is HTML escaping needed for the page to display it correctly: `&` → `&amp;`, `<` → `&lt;`, `>` → `&gt;`. Leave quotes and apostrophes as they are.

## 3. Check for duplicates

If `index.html` already has a clip with the same URL, don't add it again. Tell Tyler it's already there and stop.

## 4. Add the clip

In `index.html`, find `<ul class="clips">` in the Clips section. Add a new `<li>` using this exact pattern:

```html
        <li class="clip">
          <div>
            <h3><a href="STORY_URL">HEADLINE</a></h3>
            <p class="meta">OUTLET &middot; DATE</p>
          </div>
        </li>
```

- **DATE** uses AP style: abbreviate Aug. through Feb. (Jan., Feb., Aug., Sept., Oct., Nov., Dec.) and spell out March through July. For example, `Nov. 20, 2026` or `June 3, 2026`.
- **Order: newest first.** A new story normally goes first, directly under `<ul class="clips">`. If it's older than clips already listed, put it in date order so the list stays newest first.
- Leave out any image unless Tyler asks for one.
- Don't touch any other part of the page.

After editing, reread the new `<h3>` line and compare it with the headline you got in step 1 to make sure they match exactly.

## 5. Push so it goes live

The live site (GitHub Pages) is built from `main`.

1. Commit only `index.html`, with a message like `Add clip: <headline>`.
2. Push the current working branch: `git push -u origin <current-branch>`.
3. Push the same commit to `main`: `git push origin HEAD:main`. Tyler has approved this for this skill. If the push to `main` is rejected because `main` has commits you don't have, don't force-push. Run `git fetch origin main && git merge --no-edit FETCH_HEAD`, then push both again.
4. If a push fails for any other reason (for example, no GitHub access), tell Tyler exactly what failed. Don't say the clip is live.

## 6. Report back

Tell Tyler briefly:

- the headline, outlet and date you added (headline shown exactly)
- where it went in the list (top, or which position and why)
- that it's pushed to `main` and should appear on https://tspence11.github.io/AJI-Test-Tyler/ within a few minutes, if GitHub Pages is on
- anything you couldn't confirm
