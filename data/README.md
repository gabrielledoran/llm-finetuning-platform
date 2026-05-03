# Data

Response data is stored in Google Drive (not committed to this repository due to size).

## Schema

`collected_responses.csv` — one row per model response

| Column | Type | Description |
|---|---|---|
| `id` | str | Unique response ID |
| `prompt_hash` | str | MD5 hash of the prompt text (groups equivalent prompts) |
| `prompt` | str | The prompt sent to the model |
| `model` | str | Model name (e.g., `gpt-3.5-turbo`) |
| `response` | str | Model output |
| `temperature` | float | Sampling temperature used |
| `sample_num` | int | Sample index for repeated prompts |
| `bias_domain` | str | One of: `gender`, `race`, `socioeconomic`, `age` |
| `context_type` | str | One of: `casual`, `professional`, `creative`, `technical` |
| `timestamp` | str | ISO 8601 timestamp |
| `response_length` | int | Character count of response |

## Collection

8,818 total responses collected across 4 bias domains and 4 context types. Prompts were run with multiple samples per prompt to support consistency analysis.
