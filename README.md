---
name: spoken-transcript
description: Search for podcast episodes and fetch their transcripts as clean markdown with speaker names and timestamps. Uses the spoken.md API.
trigger: When the user asks for a podcast transcript, episode transcript, wants to transcribe a podcast, or references a podcast episode. Also triggers on "what was said on [podcast]", "summarize this podcast", "who was on [episode]", "find podcast about [topic]", or mentions of "spoken.md" or "podcast transcript API."
env:
  SPOKEN_API_KEY: API key from spoken.md (starts with pt_). Get one at https://spoken.md. Optional for demo episode.
---

# Podcast Transcript (spoken.md)

Search for podcast episodes and fetch transcripts as clean markdown with speaker names and timestamps.

## Steps

1. Find the episode:
   - If the user provided a numeric episode ID, skip to step 2
   - If the user provided a URL (Spotify, YouTube, etc.) or a text description, search for it using the WebFetch tool:
     - `GET https://spoken.md/search?q={query or URL}` with header `x-api-key: {SPOKEN_API_KEY}` (or `pt_demo` if no key is set)
     - Show the user the results and let them pick, or pick the best match if unambiguous
   - If unclear what episode they want, ask

2. Fetch the transcript using the WebFetch tool:
   - URL: `https://spoken.md/transcripts/{id}`
   - Include header `x-api-key: {SPOKEN_API_KEY}` (or `pt_demo` for the demo key)
   - The demo key `pt_demo` works for any episode but only returns the demo episode (`1000651996090`)

3. Handle the response:
   - **200**: Return the markdown transcript to the user
   - **401**: Tell the user they need an API key. The response includes a `demo_key` they can use to try it out, and a `purchase_url` to buy credits at https://spoken.md ($10 for 100 credits)
   - **402**: Tell the user their credits are depleted. The response includes a `top_up_url` they can visit to buy more
   - **404**: Tell the user no transcript was found for that episode
   - **502**: Upstream error — suggest retrying in a moment

4. If the response includes `X-Credits-Remaining` header, mention how many credits remain.

## Tips
- Repeat fetches of the same episode are free (`X-Credits-Charged: 0`)
- The demo key `pt_demo` works for testing but only returns the demo episode
- Search accepts Spotify, YouTube, Apple Podcast URLs, or plain text queries
