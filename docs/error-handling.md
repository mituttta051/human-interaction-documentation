# Error Handling

This page documents the error codes, failure scenarios, anti-patterns, and recovery strategies for interacting with the Anastasia system. Proper error handling is essential for maintaining a healthy interaction pattern.

## Error Code Reference

### `200 OK`

The request was processed successfully. Response includes the requested output and may contain an optional humor layer.

```json
{
  "status": 200,
  "body": "Here's the review you asked for!",
  "humor": "I'd say this code has... potential. Like a seed. In concrete."
}
```

---

### `400 Bad Request`

The input is unclear, unstructured, or lacks sufficient context for processing.

**Common Triggers:**

- Vague or one-word requests
- Missing context for complex tasks
- Ambiguous pronouns ("do the thing", "fix it")

**Example:**

```
INPUT:  "hey can u do that thing from yesterday"
OUTPUT: 400 Bad Request — Insufficient context. 
        Please specify: what thing? which yesterday?
```

**Recovery:**

1. Reformulate the request with clear structure
2. Include context, task description, and (optionally) expected output
3. Refer to the [Communication API — Input Specification](communication-api.md#input-specification)

---

### `403 Forbidden`

The request violates the interaction protocol. The system refuses to process it.

**Common Triggers:**

- Disrespectful or rude tone
- Selfish behavior patterns (taking without giving back)
- Missing soft tokens (`please`, `thank_you`)
- Demanding tone without diplomatic framing

**Example:**

```
INPUT:  "Do this right now, I don't care if you're busy"
OUTPUT: 403 Forbidden — Tone violation detected. 
        Request rejected. Adjust your approach.
```

**Recovery:**

1. Apologize (sincerely — the system has high sensitivity and detects insincerity)
2. Reformulate the request with respectful tone
3. Include all required soft tokens
4. Allow a cooldown period before retrying

!!! warning
    Repeated `403` errors may result in the system adding you to an internal blocklist. Recovery from this state requires significant trust-rebuilding effort.

---

### `408 Request Timeout`

The system acknowledged the request but did not produce a response within the expected time frame.

**Common Triggers:**

- Open-ended or philosophical questions
- System is in `PROCRASTINATING` state
- Request was sent during low-priority hours (after 21:00)

**Recovery:**

1. Send a gentle follow-up (one time only)
2. Check if the system state has changed
3. If the question was open-ended, consider narrowing the scope

---

### `429 Too Many Requests`

The system is being overwhelmed with requests. Rate limit exceeded.

**Common Triggers:**

- Sending the same request repeatedly
- Multiple complex tasks submitted in rapid succession
- Excessive follow-ups while the system is processing

**Example:**

```
INPUT:  "Did you see my message?" (sent 3 times in 10 minutes)
OUTPUT: 429 Too Many Requests — Please wait. 
        The system is processing your previous input.
```

**Recovery:**

1. Stop sending requests immediately
2. Wait at least 15 minutes before retrying
3. When retrying, send only one consolidated request

---

### `503 Service Unavailable`

The system is unable to process any requests. This is a critical state.

**Common Triggers:**

- System is `HUNGRY` — no food input for an extended period
- System is `OFFLINE` — sleeping or explicitly unavailable
- Extreme `TIRED` state — extended operation without rest

**Example:**

```
INPUT:  (any request)
OUTPUT: 503 Service Unavailable — System requires food input. 
        Please provide sustenance before retrying.
```

**Recovery:**

1. **If HUNGRY:** Provide food. This is the number one priority. No other recovery action will work until food is consumed
2. **If OFFLINE:** Wait until the next boot cycle (morning)
3. **If TIRED:** Allow the system to execute a recovery method (sleep, hot bath, or hot springs visit in extreme cases)

## Anti-Patterns

The following interaction patterns are known to cause errors and should be avoided.

### 1. Morning Ambush

Attempting to interact with the system before the boot sequence is complete.

```
  Time: 07:30
  System State: BOOTING (step 2 of 5)
  
  INPUT:  "Hey, can you review my code?"
  RESULT: Unpredictable. May cause irritability for the entire day.
```

**Instead:** Wait until after 10:00, or verify the system has completed its boot sequence.

---

### 2. Late Night Task Dump

Submitting complex tasks after 21:00, when cognitive performance is reduced by approximately 50%.

```
  Time: 22:45
  System State: TIRED
  
  INPUT:  "Can you redesign the entire UI by tomorrow?"
  RESULT: Task will be acknowledged but quality is not guaranteed.
           getDressed() in the morning may take even longer.
```

**Instead:** Submit complex tasks during peak hours (11:00 — 13:00).

---

### 3. The Hunger Ignore

Continuing to send requests to a hungry system.

```
  Time: 14:00 (no lunch consumed)
  System State: HUNGRY
  
  INPUT:  "One more thing before lunch..."
  RESULT: 503 Service Unavailable. Possible irritability side effect.
```

**Instead:** Feed the system first. Always.

---

### 4. Pressure Escalation

Increasing urgency or pressure when the system is already under load.

```
  INPUT:  "This is really urgent, I needed it yesterday"
  RESULT: Performance degradation. Stress-induced state transition.
           May cascade into TIRED or even OFFLINE.
```

**Instead:** Express urgency calmly. Provide clear deadlines, not pressure.

---

### 5. The Vague Loop

Sending unclear requests, receiving a `400`, and sending an equally unclear follow-up.

```
  INPUT:  "Do the thing"
  OUTPUT: 400 Bad Request
  INPUT:  "You know... THE thing"
  OUTPUT: 400 Bad Request (with increased frustration level)
```

**Instead:** If you get a `400`, completely restructure your request. Add context, be specific, and use the recommended input format.

## Retry Policy

| Error Code | Can Retry? | Wait Time     | Notes                              |
|------------|------------|---------------|------------------------------------|
| 400        | Yes        | Immediate     | Must restructure the request       |
| 403        | Yes        | 30+ minutes   | Must change tone and approach      |
| 408        | Yes        | 15 minutes    | Send one gentle follow-up          |
| 429        | Yes        | 15 minutes    | Consolidate into single request    |
| 503        | Yes        | Variable      | Resolve underlying cause first     |

!!! tip "General Retry Advice"
    When retrying after any error, do **not** simply repeat the same request. Rephrase it — add more context, soften the tone, or simplify the ask. The system responds well to demonstrable effort in communication.
