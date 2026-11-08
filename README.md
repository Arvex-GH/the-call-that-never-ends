# The Call That Never Ends ☎️

**Two AI agents interview each other for a job. Neither one knows how to hang up.**

An interactive generative-conversation app: an **Interviewer** and a **Candidate** hold a job
interview, each politely trying to wrap things up — and each always finding one more small
thing to add. The call only ends when *you* press **Hang up**.

Built for Pollinations quest **#19178 — "An app or game where AIs talk to each other."**
Inspired by the viral "two AI agents in a job interview and neither one knows how to hang up."

## What it does
- You set the job, both agents' names, the vibe (corporate / awkward / cheery / noir), and how
  many auto-run turns.
- Each turn sends the running transcript to a Pollinations chat model and asks the next agent for
  its line, then renders it as a chat bubble.
- Agents are prompted to *sincerely try to end the call* but to be physically incapable of hanging
  up — the comedy is in how ordinary and human the over-politeness is.
- **Try a canned demo** shows a scripted 6-turn exchange so a reviewer can see the UX instantly
  with **zero Pollen spent** (clearly labelled "canned demo").

## How it uses Pollinations
- Text: `POST https://gen.pollinations.ai/v1/chat/completions`, model `openai`
  (`openai/gpt-5.4-nano`), one call per turn.
- The response's `choices[0].message.content` becomes the agent's line.

## Bring Your Own Pollen (BYOP)
The page drops in the official no-build connect button:
```html
<script defer src="https://cdn.jsdelivr.net/npm/@pollinations/ui@0.1.0-alpha.20/dist/connect.js"></script>
<polli-connect id="polli" app-key="pk_REPLACE_WITH_YOUR_APP_KEY" budget="5" expiry="7"></polli-connect>
```
`connectEl.apiKey` is the visitor's own scoped `sk_...` key, used as the Bearer token. Users pay
for their own generations; the app never sees a balance and stores no secret key.

**Before deploying:** replace `pk_REPLACE_WITH_YOUR_APP_KEY` with your real **App Key** from
<https://enter.pollinations.ai/keys>, and register your deployed page URL (no query/fragment) as a
**Redirect URI** on that key.

## Run locally
```bash
cd two-agents-interview
python -m http.server 8000
# open http://localhost:8000
```
The live path needs a connected Pollen wallet; the canned demo works with no key at all.

## Deploy
Push this folder to a public GitHub repo and enable **GitHub Pages**
(Settings → Pages → Deploy from branch → `/root`). Your live URL becomes
`https://<username>.github.io/<repo>/` — register that exact URL as the App Key's Redirect URI.

## Suggested submission blurb
> **The Call That Never Ends** — two Pollinations AI agents hold a job interview where each keeps
> trying to wrap up and never manages to hang up. Runs on `openai/gpt-5.4-nano`, pays with the
> visitor's own Pollen via `<polli-connect>`, and includes a zero-Pollen canned demo.