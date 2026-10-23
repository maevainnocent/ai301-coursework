[voice-guide.md](https://github.com/user-attachments/files/33878368/voice-guide.md)
# Voice guide: how I talk upstream

## Who I am in threads

I'm a student at Howard taking AI301, making my first open-source
contributions in the Path Review repo. I'm new to this codebase, and I
say so plainly. What readers can expect from me: what I actually ran,
what I actually saw, and what I'm going to look at next. Nothing more
than that.

## Rules I write by

### Rule: Promise the investigation, not the fix

I only commit to the next thing I'm going to look at. I never promise
a fix, a PR, or a date, because I don't know yet what the fix is or
how long it will take.

- Wrong: "I'll have a fix for this up by Friday!"
- Right: "I'd like to look into this. My first step is finding where the profile form validates the URL field, and I'll post what I find here."

### Rule: Show it, don't just say it

If I say something happened, the output that proves it is pasted in
the comment. "It reproduces" with nothing under it is just a claim.

- Wrong: "Can confirm, I'm getting the same error."
- Right: "Same error on my machine. Output from `npm test` after the steps above:" followed by the pasted error.

### Rule: Name what was different about my setup

If my version, OS, browser, or steps differ from the issue's, I say
so. A difference I don't mention can make my report look like proof
of something it isn't.

- Wrong: "Reproduced the bug."
- Right: "Reproduced on the current main branch (the issue was filed on an older commit), on macOS 14 with Node 20."

### Rule: Say "I couldn't reproduce it" when that's what happened

If I can't trigger the bug, I say so, show what I got instead, and
list what might be different. I don't stretch a near-miss into a
"confirmed."

- Wrong: "I think I'm seeing the same thing, sort of."
- Right: "I couldn't reproduce this. The steps above gave me the output below with no error. One difference: I'm on Chrome, and the issue mentions Safari."

### Rule: Be specific to this issue

Every comment names something only true of this issue, like its error
message, the page or file involved, or a hint from the thread. If my
comment could be pasted onto any other issue, I rewrite it.

- Wrong: "Hi, can I work on this? Please assign me."
- Right: "I'd like to take this one. The 404 only shows up after saving a profile with an empty bio, which points me at the save handler, so I'll start there."

## Things I never post

- A promised fix, PR, or deadline ("by Friday," "in 2 days," "guaranteed")
- "+1," "same here," or "can confirm" without my own output under it
- A root cause I haven't shown evidence for ("it's definitely a race condition")
- Over-apologizing or putting myself down ("sorry, I'm a total noob, this is probably dumb")
- Comments an AI wrote that I haven't read, checked against what I actually ran, and put in my own words, or AI help I didn't disclose when the repo asks for disclosure
