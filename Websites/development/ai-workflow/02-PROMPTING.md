# Prompting the Agent — How to Get Good Results

The quality of what the agent builds depends almost entirely on how clearly you describe what you want. This guide shows you how to communicate effectively.

---

## The Golden Rule

**Describe the outcome, not the code.**

❌ "Change the CSS for the dropdown"
✅ "Make the dropdown slide down more slowly and feel more elegant"

The agent handles the code. You describe what you see, what you want, and what's wrong.

---

## Describing Visual Changes

Be specific about what you see and what you want instead. Reference:

- **Size** — "make it taller", "reduce the padding by half", "the cards should be 496px tall"
- **Color** — "the background should be white, not grey"
- **Animation** — "it should slide down with an ease, not just appear", "the open should be slower than the close"
- **Position** — "the text should be inside the image, at the bottom left", "there should be more space between the title and subtitle"
- **Behavior** — "on hover, the image should zoom in slightly, like the product carousel on the home page"

---

## Giving Feedback

After you pull and preview a change, give specific feedback:

✅ "The animation is good. The spacing between the cards needs to be wider — about double."
✅ "The title font is too small. Make it 30px and bolder."
✅ "The dropdown is visible on close when it shouldn't be. It's appearing on top of the nav."

❌ "It doesn't look right"
❌ "Fix the animation"

The more specific you are, the fewer back-and-forth rounds it takes.

---

## Batch Your Requests

If you have multiple changes, list them numbered. The agent will address all of them in one pass:

```
1. Reduce the gap between cards to 26px
2. Make the title text 30px, weight 800
3. The supporting text should be 16px
4. Remove the gradient behind the text
```

This is faster than sending one change at a time.

---

## Reference Points

If you want something to look or behave like something that already exists on the site, say so:

✅ "On hover, the image should zoom like it does on the home page product carousel"
✅ "Use the same arrow style we use everywhere else on the site"
✅ "The close button should match the one on the cart drawer"

The agent knows the existing codebase and can replicate established patterns.

---

## Confirming and Pushing

The agent will always ask before pushing. You have two options:

- Say **"push"** to approve and send it to GitHub
- Give more feedback first, and push only when you're happy

Never feel pressured to push before you're satisfied with the result.

---

## When Something Breaks

If a change causes something to look wrong or break:

1. Tell the agent exactly what you see (screenshot helps)
2. Say what it should look like instead
3. If needed, say "revert this change" — the agent can undo it

---

→ Back to [OVERVIEW.md](./OVERVIEW.md)
