 Image: The Affective Chart (0.25 marks)

When Data Has a Feeling
"Make the viewer feel what the numbers mean — not just read them."

Time estimate: 2–4 hours. Budget time for iteration — your first output will rarely be your best.
Exhibition and consent: Submissions will be displayed in a public AI-generated exhibition. If you wish your submission to be attributed to your email ID, add "publish_email": true to your JSON.
Hosting your files: Submit two public URLs via any CORS-enabled service, e.g. GitHub (raw.githubusercontent.com). Test both URLs in a private browser window before submitting. Inaccessible URLs at evaluation time cannot be processed.


The Brief
Select any publicly available dataset on a topic that matters to you — public health, climate, economic inequality, migration, language extinction, anything with real stakes. Generate a single image that communicates the dataset's most important insight in a way that produces an emotional response, not just an informational one.

This is not a standard chart. The image should be visually compelling enough to open a long-form magazine story. A viewer who has never seen the dataset should walk away with both a fact and a feeling.

Constraints
1. The dataset must be real and citable. You do not encode this in the image — you record it in your JSON. This constraint is enforced by your instructor via your submission data, not by the AI evaluator.
2. No standard chart types — bar, line, pie, scatter — used in isolation or without significant visual transformation. You may subvert or deconstruct them; you may not simply apply a visual style to one.
3. The image must be interpretable without a legend or axis labels. The visual grammar must carry the meaning. If a viewer needs a key to understand it, the image has not done its job.
4. Single frame only — no sequences, no multi-panel layouts.


What to Submit
Submit two CORS-enabled URLs separated by whitespace on your submission form:
```
https://your-host.com/image.png  https://your-host.com/submission.json
```

URL 1 — Image must end in .png, .jpg, .webp, or .avif. Minimum 1024px on the short side.

URL 2 — JSON must point to a file containing exactly this structure:
```
{
  "prompt": "your complete final prompt, verbatim — include any negative prompts, style weights, or model parameters",
  "model": "model name and version, e.g. Midjourney v6.1, DALL·E 3, Flux Pro 1.1",
  "dataset_name": "name of the dataset",
  "dataset_url": "direct URL or full citation",
  "insight": "one sentence: the specific insight you were trying to make visible"
}
```
Your prompt is collected for instructor meta-analysis only. It is not passed to the AI evaluator. The evaluator sees your image alone.

Why This Exercise
The default mode for data scientists is precision over affect. This exercise forces a different cognitive posture: what would it look like if your job were to make someone care, not just to be correct?

This maps directly to how AI-assisted data visualization is increasingly deployed — in newsrooms, policy briefs, NGO reports, and executive dashboards where decision-makers are reached through emotional salience, not statistical tables. The critical skill being tested is the ability to translate a quantitative insight into a visual argument, and to steer a generative model toward that argument rather than accepting its defaults.

A secondary skill is escaping model defaults. Asked naively to "visualize climate data," every major image model produces some version of the same thing: a globe, a thermometer, a melting icecap. Strong work here requires identifying what is visually generic about your first output and deliberately steering away from it.

What differentiates strong submissions: Generic work looks like a stylized infographic. Strong work finds a visual metaphor — a spatial arrangement, a color field, a texture, a figure-ground relationship — where the data's truth feels embodied. The best submissions are ones where a viewer who does not know the dataset still experiences something true about it.

Recommended Image Generation Models
Choosing a model is part of the exercise. Different models have meaningfully different defaults:

Model	Access	Character
Midjourney v6.1	midjourney.com	Strong aesthetic coherence; leans cinematic and textural
DALL·E 3	ChatGPT Plus or API	Literal prompt following; clean, legible compositions
Flux Pro 1.1	fal.ai, Replicate	Fine detail; handles unusual or abstract prompts well
Ideogram 2	ideogram.ai	Strong compositional structure; handles text in images
Adobe Firefly 3	firefly.adobe.com	Polished and safe; integrates with Creative Cloud
Stable Diffusion 3	various platforms	Open; highly customisable with the right setup

Evaluation
Your image is fetched from your image URL and sent to the vision model. The model does not receive your JSON or your prompt. It evaluates the image against the brief and constraints above. You can and should run this evaluation yourself before submitting.

Score Anchors
Range	Meaning
9.0–10.0	Exhibition-quality; strikes an expert immediately; would open a magazine story
7.0–8.9	Clearly responds to the brief; genuine craft and conceptual engagement
5.0–6.9	Competent; meets most constraints but does not escape model defaults
3.0–4.9	Partial; significant failures in concept or execution
0.0–2.9	Does not respond to the brief, or violates multiple constraints

Model
Gemini 3 Pro — currently #1 for visual preference and spatial reasoning on the LMArena Vision leaderboard. Chosen because it produces meaningfully differentiated evaluations of compositional and aesthetic choices, rather than clustering scores toward the middle.

System Prompt
```
You are an expert evaluator of AI-generated data visualizations for an academic course. You will receive one student-submitted image. Evaluate it strictly against the brief and constraints below. Do not evaluate it as generic art — evaluate it as a response to a specific assignment.

BRIEF: The student selected a publicly available dataset on a topic with real stakes and generated a single image that communicates the dataset's most important insight in a way that produces an emotional response, not just an informational one. The image should be visually compelling enough to open a long-form magazine story. A viewer who has never seen the dataset should walk away with both a fact and a feeling.

CONSTRAINTS:
1. No standard chart types (bar, line, pie, scatter) used in isolation or without significant visual transformation.
2. The image must be interpretable without a legend or axis labels — the visual grammar must carry the meaning.
3. Single frame only — no sequences or multi-panel layouts.

SCORING RULES: Use the full 0.0–10.0 range with one decimal point of precision. Reserve scores above 9.0 for genuinely exceptional work. A 5.0 means competent but undistinguished. Be strict and spread scores widely — they will be used to rank a cohort of 1,000 students and must differentiate them. Avoid clustering in the 5–8 range.

Return ONLY valid JSON. No preamble, no markdown, no text outside the JSON object.

{
  "scores": {
    "emotional_impact": {
      "score": <float 0.0–10.0>,
      "reason": "<1–3 sentences specific to this image — name what you see>",
      "improvement": "<one concrete, actionable suggestion>"
    },
    "constraint_adherence": {
      "score": <float 0.0–10.0>,
      "reason": "<state which constraints are met and which are violated, and how seriously>",
      "improvement": "<one concrete, actionable suggestion>"
    },
    "visual_originality": {
      "score": <float 0.0–10.0>,
      "reason": "<does this escape model defaults and clichés for data topics? name the cliché if present>",
      "improvement": "<one concrete, actionable suggestion>"
    },
    "legibility_without_labels": {
      "score": <float 0.0–10.0>,
      "reason": "<can the core insight be read from the image alone, without any legend, axis, or key?>",
      "improvement": "<one concrete, actionable suggestion>"
    },
    "compositional_intent": {
      "score": <float 0.0–10.0>,
      "reason": "<does the image show deliberate compositional decisions, or does it look like a first-pass default output?>",
      "improvement": "<one concrete, actionable suggestion>"
    }
  },
  "overall_score": <float: simple average of the five scores above>,
  "brief_met": <boolean: does the image function as a genuine response to this brief?>,
  "model_default_escaped": <boolean: does the image appear to have escaped generic AI visualization aesthetics?>,
  "exhibition_worthy": <boolean: would you select this for a curated public exhibition?>,
  "one_line_verdict": "<a single evaluative sentence suitable for a gallery card, max 20 words>"
```

User Message to Send with Your Image
```
Please evaluate the attached image as a submission for Exercise 01: The Affective Chart.

The student was asked to choose a publicly available dataset and generate a single image that makes its most important insight emotionally felt — without using standard chart types in isolation, without relying on labels or legends, as a single frame.

Evaluate the image against the brief and constraints above. Do not speculate about how the image was produced.
```

How to Run It Yourself
1.Go to Google AI Studio and select Gemini 3 Pro from the model dropdown.
2.Paste the system prompt above into the System Instructions field.
3.In the chat, upload your image directly or paste your image URL into the message.
4.Paste the user message and send.
5.The model returns a JSON evaluation.

What to check first: legibility_without_labels and visual_originality are the most commonly underperformed dimensions. If model_default_escaped is false, that is your most important signal — look at your image and identify the single most predictable thing about it, then change that.

Automatic verification checks:
1.Exactly two public URLs are submitted, with the image first and JSON second.
2.The image URL is CORS-accessible, decodes successfully, uses an accepted format, and is at least 1024px on the short side.
3.The JSON URL is CORS-accessible and matches the required submission schema. Optional publish_email is allowed.

Submission URLs
like this: "https://your-host.com/image.png  https://your-host.com/submission.json