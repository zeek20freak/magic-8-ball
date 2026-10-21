# Magic 8 Ball

A plastic ball that answers yes-or-no questions with a real probability instead of a canned fortune.

## What this is

One HTML file. You type a yes-or-no question, optionally add the facts that matter, and the ball asks a decision model — **Drex v1.5**, served through OpenRouter's Decisions API — for P(yes). The model returns an actual probability from a single forward pass. The ball translates that probability into a classic 8-ball-style reading and prints the real percentage underneath it.

It also asks the model a second question: *can this question even be answered yes/no from these facts?* If that score comes back low, the ball says "Ask again later" instead of dressing up a coin flip as wisdom.

## What it is not

- **Not a fortune teller.** The probability is the model's judgment on the facts you handed it. Thin facts in, thin probability out.
- **Not advice.** It's a toy that shows its number.
- **Not finished.** This is a proof of concept, built fast, and it doesn't pretend otherwise.

## Run it

Open `index.html` in a browser. No build step, no server, no dependencies. (Fonts load from Google Fonts when you're online; everything else lives in the file.)

You need your own OpenRouter API key: https://openrouter.ai/settings/keys

Paste it into the page. The key is held only in the tab's memory and sent directly from your browser to OpenRouter. It is never stored — there is no backend here to store it in. Each shake is one small API call and costs whatever OpenRouter charges for it.

## How the readings map

| P(yes) | Reading |
|---|---|
| *(question not answerable)* | Ask again later |
| ≥ 0.90 | Without a doubt |
| ≥ 0.78 | Outlook is strong |
| ≥ 0.62 | Signs point to yes |
| ≥ 0.54 | Leaning yes |
| ≥ 0.46 | Reply hazy |
| ≥ 0.38 | Leaning no |
| ≥ 0.22 | Outlook is doubtful |
| ≥ 0.10 | Very doubtful |
| < 0.10 | Do not count on it |

"Not answerable" fires when the model's answerability score drops below 0.42 — the question isn't yes/no shaped, or the facts are too thin to judge.

## Make a better version

This repo is a **proof-of-concept playground**, not a product. The idea worth taking is the shape: a narrow, playful door onto a model that returns calibrated uncertainty instead of a paragraph. This implementation is just the simplest version that works. Fork it and do better:

- Put a different model behind the ball and compare its calibration against Drex's.
- Change the thresholds, or replace the reading buckets with your own.
- Log questions and outcomes, then score the ball's calibration for real.
- Give it a better handle — voice in, shake the phone, anything that lets a stranger use it in one gesture.

If you build something better, that was the point.

## The door idea, in one paragraph

Most AI interfaces hand you the whole model and a blank text box. This is the opposite: one gesture, one typed judgment, an honest number underneath. A narrow door, on purpose. Whether doors like this — small, single-purpose, honest about their uncertainty — are a good way for people to use models is the actual experiment. The ball is just the first one built to test it.

## License

MIT. Take it, fork it, ship the better one.

## Honesty note

I don't know how to code. This was built by an AI (Quine, running on Muse) with my guidance: I described what I wanted, made the design decisions — a probability, not a story; the user's key never leaves their browser — and tested whether the thing actually worked. The AI wrote every line of code. I can't read it, and I don't claim to understand how the program works under the hood. By the common definition, that makes this slop — code shipped by someone who can't read it — and I'd rather print that in the repo than let anyone assume otherwise. It's here as a proof of concept, labeled as what it is. Read the code yourself before trusting it. And if you can build it better, that's the invitation at the top of this file.
