# spoken.md — Claude Code Skill
 
Fetch any podcast episode as a clean, speaker-labeled Markdown transcript. One API call from inside Claude Code. 
 
## Install 

```bash
claude install-skill https://github.com/roberttomko/spoken.md
```
 
Or add the skill manually to your project's .claude/skills/ directory.
 
Setup
 
Get an API key at https://spoken.md ($10 for 100 transcripts), then set it as an environment variable: 

# In your Claude Code settings or shell profile
export SPOKEN_API_KEY=pt_your_key_here
 
Or try it free with the built-in demo key pt_demo (returns one sample episode).

Usage

Once installed, just ask Claude Code for a podcast transcript: 
 
- "Get me the transcript of the Huberman Lab episode with Matt Walker" 
- "Transcribe this episode: https://open.spotify.com/episode/..."
- "Fetch podcast transcript for episode 1000651996090"
- "Search for podcast episodes about sleep science"
 
Claude will automatically search for the episode, fetch the transcript, and return clean Markdown with speaker names and timestamps. 

What you get 

**Andrew Huberman** (0:00)
Welcome to the Huberman Lab podcast,
where we discuss science and science-based 
tools for everyday life.
 
**Matt Walker** (0:45)
Thank you for having me, Andrew. Sleep is
one of those things where small changes to
your routine can have outsized effects on
both mental and physical health.

Pricing
 
- Free: Use pt_demo to try with a sample episode 
- $10: 100 transcripts ($0.10 each). Repeat fetches of the same episode are free
- No subscription: Credits never expire
 
Get your key at https://spoken.md. 
 
Links

- https://spoken.md/docs.html
- https://spoken.md/.well-known/openapi.json
- https://spoken.md/llms.txt
