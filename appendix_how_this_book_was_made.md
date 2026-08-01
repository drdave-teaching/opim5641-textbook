# Appendix — How This Book Was Made

Students ask, so here's the honest answer - and it doubles as a case study in the exact human-plus-AI workflow this course wants you to learn.

## The pipeline

1. **I record real lectures.** Screen + voice, walking through the same notebooks you run. Nothing in this book started as text - it started as teaching.
2. **Machine captions.** UConn's Kaltura service auto-transcribes each video (the same captioning you see in the player). Raw machine captions are about 95% right and 100% unpolished - "loc" becomes "lock," equations become soup.
3. **AI polishing.** I work with an AI assistant (Claude) to turn the raw captions into clean, first-person scripts - fixing the mis-hearings, keeping my voice, my jokes, and my digressions. Every script is labeled "AI-polished from auto-captions."
4. **Chapters get woven.** The book's prose is built from those scripts plus the *actual code* in the course notebooks - so what you read matches what you run. The notebooks themselves are executed end-to-end before every update; if "Runtime → Run all" breaks, it doesn't ship.
5. **Jupyter Book + GitHub.** The whole book is Markdown in a public GitHub repository, built with [Jupyter Book](https://jupyterbook.org) and deployed automatically by GitHub Actions to GitHub Pages every time a commit lands. There is no hidden CMS - the [source](https://github.com/drdave-teaching/opim5641-textbook) is right there.

## Why do it this way?

- **Accessibility.** Every lecture exists as searchable, skimmable text - not just 10 minutes of video you can't Ctrl+F.
- **One source of truth.** Notebooks, book, and videos stay in sync because they're built from each other, in version control.
- **Speed with verification.** AI does in minutes what used to take me a semester of evenings. But notice the shape of the workflow: *the expertise and the teaching are mine; the AI accelerates and I verify.* Numbers in worked examples are computer-checked. Notebooks are run before publishing. Polished scripts are diffed against what I actually said.

## The meta-lesson

This is the same deal I offer you in the course: use Claude, ChatGPT, Gemini - go bigger and faster than you could alone. But the understanding stays YOUR deliverable. If you can't explain what the code does, you didn't do the work - you just watched it happen. The book you're reading is proof the workflow can be honest: human judgment at every gate, AI in the loop, everything verifiable in public.

*Found an error? The repo takes [issues](https://github.com/drdave-teaching/opim5641-textbook/issues) - catching a real mistake in the book is worth bragging rights.*
