# Communication API

This page documents the supported communication methods, input/output specifications, and protocol requirements for interacting with the Anastasia system.

## Base Channels

All interactions are routed through the following channels:

| Channel       | Protocol    | Availability           |
|---------------|-------------|------------------------|
| Text Message  | Asynchronous| 10:00 — 23:00         |
| Voice Message | Asynchronous| 10:00 — 23:00         |
| In-Person     | Synchronous | When system is nearby   |

## Authentication

No formal authentication is required, but all requests must include the following **soft tokens**:

- `please` — required in the request body
- `thank_you` — required upon receiving a response
- `respectful_tone` — must be set to `true` for the entire session

!!! danger "Unauthorized Access"
    Requests missing soft tokens or containing disrespectful/selfish patterns will be silently dropped or returned with a `403 Forbidden` response.

## Methods

### `POST /ask`

Used for direct questions that expect a specific answer.

**Request:**

```json
{
  "method": "ask",
  "question": "How does the ECS pattern work in game engines?",
  "context": "Working on our Unity project",
  "tone": "polite",
  "urgency": "normal"
}
```

**Response:**

```json
{
  "status": 200,
  "body": "Structured explanation with relevant details",
  "extras": {
    "humor": "optional pun or sarcastic remark",
    "follow_up": "Would you like me to show you an example?"
  }
}
```

**Response Time:** ~5 minutes (text), immediate (in-person)

---

### `POST /request`

Used for task delegation. The system will process the task and return a result.

**Request:**

```json
{
  "method": "request",
  "task": "Review the pull request for the inventory system",
  "context": "Sprint deadline is Friday",
  "expected_output": "List of comments and suggestions",
  "incentive": "chocolate_sweets",
  "tone": "polite"
}
```

**Response:**

```json
{
  "status": 200,
  "body": "Detailed review with actionable feedback",
  "quality": "high",
  "delivery_time": "varies based on system state and task complexity"
}
```

!!! note "Performance Hint"
    Setting the `incentive` field to `"chocolate_sweets"` or `"hot_chocolate"` has been empirically shown to reduce delivery time.

---

### `POST /discuss`

Used for open-ended conversations, brainstorming, or social interaction. This method may trigger the `SOCIAL` state.

**Request:**

```json
{
  "method": "discuss",
  "topic": "What if we added a cooking minigame to our project?",
  "mood": "casual",
  "tone": "friendly"
}
```

**Response:**

```json
{
  "status": 200,
  "body": "Enthusiastic response with multiple creative suggestions",
  "side_effects": [
    "may generate follow-up ideas unprompted",
    "humor_level: elevated",
    "possible state transition to SOCIAL"
  ]
}
```

**Response Time:** Variable. Open-ended discussions may have longer initial processing time (up to several hours for complex topics) but produce richer output.

---

### `POST /feedback`

Used to provide feedback on previous outputs. Positive feedback is a performance multiplier.

**Request:**

```json
{
  "method": "feedback",
  "type": "positive",
  "message": "The chocolate cake was amazing, thank you!"
}
```

**Response:**

```json
{
  "status": 200,
  "body": "Thank you! :)",
  "mood_effect": "+comfort, +motivation"
}
```

!!! warning
    Negative feedback must be delivered with a `diplomatic` flag set to `true`. Blunt or aggressive negative feedback may cause unexpected system behavior.

## Input Specification

All requests should follow this general schema:

| Field             | Type     | Required | Description                                  |
|-------------------|----------|----------|----------------------------------------------|
| `context`         | string   | Recommended | Background information for the request    |
| `task` / `question` | string | **Yes**  | The actual request or question               |
| `expected_output` | string   | Optional | Desired format or content of the response    |
| `tone`            | enum     | **Yes**  | Must be `"polite"` or `"friendly"`           |
| `urgency`         | enum     | Optional | `"low"`, `"normal"`, `"high"`                |
| `incentive`       | string   | Optional | Performance booster (e.g., `"chocolate"`)    |

## Output Specification

All responses include the following fields:

| Field         | Type     | Description                                |
|---------------|----------|--------------------------------------------|
| `status`      | integer  | HTTP-style status code                     |
| `body`        | string   | Primary response content                   |
| `humor`       | string   | Optional humor layer (sarcasm or pun)      |
| `follow_up`   | string   | Optional suggestion for next interaction   |

## Rate Limits

| Condition                        | Limit                              |
|----------------------------------|------------------------------------|
| Normal operation                 | No hard limit                      |
| During `TIRED` state             | Max 3 complex tasks per hour       |
| During `FOCUSED` state           | Unlimited (within scope of focus)  |
| After 21:00                      | Best-effort only; no SLA           |
| Repetitive identical requests    | `429 Too Many Requests` after 3rd attempt |

## Response Latency

| Request Type     | Average Latency         | Notes                          |
|------------------|-------------------------|--------------------------------|
| Simple question  | ~5 minutes              | Via text                       |
| Complex question | Up to several hours     | Open-ended or philosophical    |
| Task delegation  | Depends on task scope   | May trigger `FOCUSED` state    |
| In-person query  | Immediate               | Highest priority channel       |
