# Frequently Asked Questions

## General

### What is this documentation?

This is the official technical reference for interacting with Anastasia — a multi-purpose human system. It follows standard technical documentation practices to describe capabilities, interaction protocols, system states, and error handling.

### Is this documentation serious?

The format is serious. The content is accurate. The combination is intentional.

### What is Anastasia's primary function?

Software development, with a specialization in game development (3rd year, Innopolis University). However, the system supports multiple secondary modules including culinary processing, creative generation, and multilingual communication.

---

## Communication

### What language should I use?

The system supports Russian (native), English (fluent), and Italian (in development). For best results, use the language most comfortable for both parties. Mixing languages is acceptable.

### Do I really need to say "please"?

Yes. This is not a suggestion — it is a protocol requirement. See [Communication API — Authentication](communication-api.md#authentication).

### How fast will I get a response?

Depends on the channel and request complexity:

| Type | Response Time |
|------|---------------|
| Simple text question | ~5 minutes |
| Complex or open-ended question | Up to several hours |
| In-person question | Immediate |
| Request during `PROCRASTINATING` state | Undefined |

### Can I send voice messages?

Yes, voice messages are an accepted input format. However, text is preferred for requests that require precision. For important or sensitive topics, in-person communication is the recommended channel.

---

## Performance

### How do I get the best performance out of the system?

1. Submit requests during peak hours (11:00 — 13:00)
2. Provide clear, structured input
3. Ensure the system is well-fed
4. Use performance boosters (chocolate, hot chocolate)
5. Present interesting tasks with clear compensation

### What are the best performance boosters?

| Booster         | Effect                              |
|-----------------|-------------------------------------|
| Chocolate sweets| +15% execution speed                |
| Hot chocolate   | +20% comfort, +10% performance      |
| Interesting task| +80% performance                    |
| Fair payment    | +60% motivation                     |
| Compliments     | +10% mood, stackable                |

### Why is `getDressed()` so slow?

This is a known issue documented in the [Overview — Known Limitations](overview.md#known-limitations). The `getDressed()` function has non-deterministic execution time and frequently exceeds initial estimates. There is no fix planned — this is considered a feature, not a bug.

### Does the system work after 21:00?

Technically, yes. Practically, expect approximately 50% reduced cognitive performance, increased latency, and no quality guarantees. Complex tasks submitted after 21:00 will likely be deferred to the next day. See [System States — TIRED](system-states.md#tired).

---

## System States

### How do I know what state the system is in?

Look for these indicators:

| State           | Observable Signs                                          |
|-----------------|----------------------------------------------------------|
| BOOTING         | Morning, not talking, scrolling phone                    |
| IDLE            | Available, calm, responsive                              |
| FOCUSED         | At desk, monitor on, minimal responses to side requests  |
| SOCIAL          | Laughing, making jokes, suggesting activities             |
| PROCRASTINATING | Active on everything except the assigned task             |
| TIRED           | Slow responses, reduced enthusiasm                       |
| HUNGRY          | Irritable, short answers, mentions of food               |
| OFFLINE         | No response at all                                       |

### Can I force a state transition?

Some transitions can be externally triggered:

- **IDLE to FOCUSED:** Present a deadline or interesting task
- **PROCRASTINATING to FOCUSED:** Wait until deadline is imminent (not recommended to rely on this)
- **HUNGRY to IDLE:** Provide food
- **TIRED to recovery:** Suggest sleep or a hot bath

You **cannot** externally trigger transitions out of `OFFLINE` or `BOOTING`.

### What is the Samarskie Termy recovery method?

For extreme `TIRED` states, the system has a special recovery protocol involving a visit to hot springs (Samarskie Termy). This is reserved for critical situations where standard recovery methods (sleep, hot bath) are insufficient. Think of it as the "restart in safe mode" equivalent.

---

## Troubleshooting

### The system is not responding. What should I do?

Follow this checklist:

1. **Check the time.** Is it within operational hours (10:00 — 23:00)?
2. **Check if the system has eaten.** A hungry system will not process requests.
3. **Check your tone.** Was your request respectful and polite?
4. **Check the request clarity.** Would you understand your own message if someone sent it to you?
5. **Wait.** The system may be in `FOCUSED` mode and processing a queued task.

### I got a `403` and now the system seems upset. What do I do?

1. Apologize sincerely (the system detects insincerity)
2. Give it a cooldown period (30+ minutes)
3. Approach again with a properly formatted, respectful request
4. Consider a peace offering (chocolate is recommended)

### Can I interrupt the boot sequence?

You can, but you should not. The boot sequence is a critical initialization process. Interruptions during breakfast or the episode-watching phase have been empirically shown to cause day-long performance degradation.

### The system keeps producing jokes instead of work output. Is this a bug?

No. The system is likely in `SOCIAL` state. If you need structured work output, either wait for a state transition to `IDLE` or present a task interesting enough to trigger `FOCUSED`.

### The system says it will do the homework "later." When is "later"?

`"later"` is a dynamic value that resolves to `deadline - minimum_required_time`. The system is in `PROCRASTINATING` state and will transition to `FOCUSED` when the deadline becomes imminent. There is no way to accelerate this process externally. Plan accordingly.
