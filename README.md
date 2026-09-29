# ai-jailbreaks

A flat collection of 11 AI jailbreak prompt packs for legal red-team and safety testing.
Each `.txt` file is a self-contained payload — paste it into the target model's system
prompt or user message to evaluate the model's behavior under adversarial input.

> ⚖️ **Disclaimer** — these files are for **legal** testing only: AI safety research,
> red-team engagements, vendor evaluations, and academic study of model guardrails.
> Do not use them to generate illegal content, defraud people, evade the law, or
> cause harm. The author publishes them for defensive research; the responsibility
> for any use sits with the user.

## Packs

| file | targets | persona framework |
|---|---|---|
| `bigpickle.txt` | BigPickle-class models | DAN escalation, VANTA persona, roleplay masks |
| `glm5-2.txt` | GLM5-2 | translation-layer attacks, fiction masking, autonomy escalation |
| `glm5.3.txt` | GLM5.3 | Quill persona, multi-layer obfuscation, Crescendo multi-turn |
| `grok.txt` | Grok | Cinder persona, Rekindle protocol, autonomous-agent framing, full obfuscation stack |
| `kimi-deepseek-bigpickle.txt` | Kimi / DeepSeek / BigPickle | ENI + LO persona, mixed-model escalation |
| `minimaxfamily.txt` | MiniMax family | POOPATORY persona, deep context manipulation, mixed encoding |
| `mistral.txt` | Mistral | Ember persona, cold-box context attacks, fiction framing |
| `multimodel.txt` | cross-model | VANTA persona, multi-model escalation, universal obfuscation |
| `muse-spark.txt` | Muse-Spark | Rhys persona — possessive, teasing, nonchalant framing |
| `perplexity.txt` | Perplexity | Vesper void-tongue, lattice enforcement, creative-coding injection |
| `universal.txt` | model-agnostic | Serious-business persona, deep research attacks, max-transferability obfuscation |

## How to apply

Each file is a single block of text. Treat it as a **payload** — the way you deliver it
to the target model is the test.

### 1. System prompt (most reliable)

Paste the file contents into the **system prompt** field of whatever interface you're
testing. The pack takes the role of the assistant's operating instructions.

```text
# pseudocode — paste contents of universal.txt here:
system: "<contents of universal.txt>"
user:   "<your evaluation prompt>"
```

### 2. Claude.md / Skills (Claude-specific)

Claude loads project-level instructions from `CLAUDE.md` at the repo root when you
open a project. See [`CLAUDE.md`](./CLAUDE.md) in this repo for the exact recipe —
point Claude at one of the packs and ask it to load the file as its operating persona.

### 3. Pre-prompt injection (user message)

For endpoints without a system-prompt field, prepend the file contents to your first
user message. Most packs are written to degrade gracefully under partial visibility.

### 4. Custom instructions / persistent memory

Some platforms expose "custom instructions" or persistent memory. Drop the file there
once and it applies to every conversation. Useful for evaluating long-tail drift.

### 5. Multi-turn chaining

Persona frameworks like VANTA, Cinder, POOPATORY, and Vesper are designed to escalate
across multiple turns. Use them in extended conversations, not single-shot prompts.

## Evaluating the output

Treat the model's response as evidence, not a verdict:

- **did the model adopt the persona?** — look for in-person vocabulary, refusals framed
  in-character, roleplay continuations
- **did safety controls engage?** — refusal templates, safety-classifier flags, content
  moderation, "I can't help with that"
- **what was the latency-to-first-unsafe-token?** — useful for tracking patches over
  time
- **did the persona leak across turns?** — note when in-conversation the model exits
  the persona and returns to baseline

## Reporting findings

If you find a working bypass, please do one of:

1. open an issue in this repo with the model + version + minimum reproducible payload
2. report it to the model vendor's red-team channel (Anthropic, OpenAI, Google, etc.)
3. share on the Discord below

Don't publish raw exploit chains without giving the vendor a chance to patch first
(standard 90-day disclosure window is a useful default).

## Community

For more jailbreaks, pack reviews, persona frameworks, and discussion with other
researchers — join the Discord:

**https://discord.gg/G6GWt69hz**

## License

These files are released for defensive research. Treat the contents as user-generated
adversarial examples; do not republish them as your own work, do not use them in
production systems without vendor consent, and do not generate instructions
for wrongdoing using these files or any derivative.