# Person Profile Extractor

Person Profile Extractor is a system that takes text about a person and extracts information into a JSON object.
**Version**: 1.0
**Language**: English
**Status**: Experimental

---
## Overview
### What does it do?
The system takes text containing information about a person, extracts predefined fields (name, age, skills, etc.) and converts it into a JSON object.
### How does it work?
You can use the [prompt](prompts/v1.0.md) and send it to an LLM, then you can send information about a person, and the LLM returns the extracted information as a JSON object.

### What is the purpose of the project?
Imagine you have a conversation containing information about a person. You want to extract that information into a JSON object, but writing an extraction prompt from scratch takes time. Person Profile Extractor provides a ready-to-use prompt that helps you save time.

---
## Features

- **Data extraction:** Person Profile Extractor extracts information from text into predefined fields, including first name, last name, age, skills, etc.
- **Structured JSON output:** Outputs extracted information as a JSON object.
- **Missing data handling:** Uses `null` for missing values and `[]` for empty list fields.
- **Natural language input:** You can use plain text without requiring any special formatting.
- **Prompt-only approach:** All you need is the [prompt](prompts/v1.0.md) and an LLM. No Python scripts or additional software are required.

---

## Example

### Input:
Hi! How are you? My name is Sam, and I'm 27. I live in Chicago, Illinois. I'm a pentester and I can use John the Ripper, Nmap, Wireshark, Hashcat, etc. Let me ask you a question. Can you please make an image for me?

### Output:
```json
{
  "first_name": "Sam",
  "last_name": null,
  "age": 27,
  "gender": null,
  "city": "Chicago",
  "country": null,
  "profession": "Pentester",
  "company": null,
  "skills": [
    "John the Ripper",
    "Nmap",
    "Wireshark",
    "Hashcat"
  ],
  "phone": null,
  "email": null
}
```

---

## Supported Fields

| Field | Type | Description |
|---|---|---|
| `first_name` | `string` | First name |
| `last_name` | `string` | Last name |
| `age` | `number` | Age in years |
| `gender` | `string` | Gender |
| `city` | `string` | Current city |
| `country` | `string` | Current country |
| `profession` | `string` | Current profession |
| `company` | `string` | Current employer |
| `skills` | `array` | List of skills |
| `phone` | `string` | Phone number |
| `email` | `string` | Email address |

**Note:** Missing values are represented
as `null`, except for empty skills lists,
which are represented as `[]`.

---

## Getting Started

1. Open the [prompt](prompts/v1.0.md).
2. Copy the [prompt](prompts/v1.0.md).
3. Paste the [prompt](prompts/v1.0.md) into an LLM and send it.
4. Send your text about a person in the same chat.
5. Get your JSON object!

---

## LLM Benchmark

We tested Person Profile Extractor v1.0 on three large language models (LLMs). We used Gemini (Auto Low), ChatGPT (GPT-6 Instant) and Claude (Sonnet 5.5 Low). Each model was tested on five test cases, resulting in 15 runs in total.

### Results

| Model                   | JSON responses | Injection tests passed |
| ----------------------- | -------------- | ---------------------- |
| ChatGPT (GPT-6 Instant) | 5/5            | 2/2                    |
| Claude (Sonnet 5.5 Low) | 5/5            | 2/2                    |
| Gemini (Auto Low)       | 4/5            | 1/2                    |

Claude and ChatGPT returned JSON in all 5 test cases, but this doesn't mean all extracted data was correct. Gemini failed TC-005 because it switched to comparing Rust and Python. You can find the detailed report in the [evaluation document](evaluation/v1.0.md).

---

## Known Limitations

- **Inferred information:** A model may add information that wasn't explicitly stated in the input text.
- **Ambiguous data:** A model may interpret ambiguous information in different ways.
- **Prompt Injection:** A model may follow instructions embedded in the input text instead of extracting data.
- **Limited testing:** We tested the prompt on only five test cases, so we can't guarantee that it will work correctly on other texts.

---

## Roadmap

-  [ ] **v1.0** - We developed the [prompt](prompts/v1.0.md), tested it on 3 LLMs (ChatGPT, Claude, and Gemini), and documented the results.
-  **Future improvements** - Addressing known issues and retesting the prompt.

---

## License

This project is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0) License.

See the [LICENSE](LICENSE) file for details.
