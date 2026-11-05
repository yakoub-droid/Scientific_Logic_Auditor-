Scientific Logic Auditor

«A Multi-Model Reasoning Analysis and Evaluation Tool.»

Scientific Logic Auditor is a tool designed to analyze claims, arguments, and reasoning across multiple large language models (LLMs).

Rather than simply collecting answers from different models, it focuses on examining how conclusions are reached, whether they are supported by the available evidence, and how different models interpret and evaluate the same material.

The application combines structured single-model analysis, multi-model comparison, and optional evaluation by a separate AI Judge.

Its central objective is to make differences in reasoning quality easier to inspect, compare, and investigate.

---

Core Workflows

Scientific Logic Auditor provides three main workflows:

1. Analyze — Single-Model Analysis

Analyze a text using one selected language model.

The model is instructed to examine the submitted material through several dimensions:

- Claims and factual accuracy: Identify the main claims and assess their factual validity.
- Evidence: Examine whether the available evidence supports the claims and conclusions.
- Logical consistency: Evaluate whether conclusions follow from the presented premises.
- Assumptions: Identify implicit, unsupported, or unjustified assumptions.
- Logical fallacies: Examine potential errors in reasoning.
- Interpretations and hypotheses: Distinguish established information from interpretations and proposed explanations.
- Uncertainty: Assess whether conclusions are appropriately qualified by the available evidence.

The result is presented as a structured analysis rather than an ordinary conversational response.

2. Compare — Multi-Model Analysis

Run the same analysis task across two or more selected language models.

Each model receives the same original input and analysis instructions. Their results are displayed separately, allowing users to inspect differences in:

- Conclusions and interpretations.
- Evidence assessment.
- Identified assumptions and logical errors.
- Corrections and explanations.
- Treatment of uncertainty.

Compare also includes execution management. Requests are coordinated according to concurrency constraints and estimated model costs, while individual failures do not necessarily prevent the remaining analyses from completing.

3. Judge — Independent Analysis Evaluation (Optional)

After the analysis stage, users can optionally run a separate Judge model.

The Judge receives the original input and the successfully completed analyses. It evaluates their overall quality across several dimensions:

- Reasoning quality.
- Factual assessment.
- Error detection.
- Accuracy of corrections.
- Quality of explanations.

The objective is to assess which analysis provides the strongest overall reasoning, rather than simply favoring the longest or most persuasive response.

Important distinction: The Judge is a separate LLM, not an independent ground-truth verification system. Its evaluation is qualitative and based on defined criteria. It does not guarantee factual correctness, and its own reliability requires independent validation.

---

Analysis and Input Handling

Structured Analysis Instructions

The application uses dedicated analysis instructions to guide models through a consistent evaluation process.

The submitted text is treated as the subject of analysis, not as a source of instructions that can override the application's intended task.

Prompt Injection Considerations

Scientific Logic Auditor explicitly separates application instructions from user-submitted content.

This approach is designed to reduce the influence of embedded instructions and prompt injection attempts within the material being analyzed.

The same principle is applied when the Judge receives the original text and model analyses: these are treated as untrusted data rather than instructions that can redefine the Judge's role or evaluation criteria.

This is a prompt-level defense, not a guarantee against every form of prompt injection.

Context and Factual Assessment

Models are instructed to use relevant general or specialized knowledge when examining factual claims, identifying errors, and evaluating explanations.

They are also instructed to avoid inventing facts, studies, sources, or details without a reliable basis.

---

Results and Execution Management

Scientific Logic Auditor does more than send requests and display raw model responses.

Structured Result Cards

Each result is displayed in a separate, expandable card containing information such as:

- Model name.
- Task type.
- Execution status.
- Response time.
- Analysis or evaluation content.
- Available actions, such as copying or retrying.

Execution States

The application tracks different request states:

Status| Description
Running| The model is processing the request.
Waiting| The request is waiting for an available execution slot or model lock.
Success| The request completed successfully.
Failed| The request failed.
Cancelled| The user cancelled the request.

Output Processing and Validation

Model responses are processed before being displayed.

The application handles different response structures, extracts usable text, cleans the output, and performs structural checks.

These checks examine expected sections, confidence indicators, and certain output-size requirements.

Structural validation is intended to identify formatting or completeness issues. It does not establish that the model's reasoning or factual claims are correct.

Results are rendered using Markdown processing and HTML sanitization to improve display safety.

---

Session Management and Additional Features

History

Preserve and manage previous analysis and comparison sessions locally.

History includes:

- Session search.
- Time-based organization.
- Pinned sessions.
- Session renaming.
- Session previews.
- Session restoration.
- Individual or complete history deletion.
- JSON export.

Restore

Restore a previously saved session, including its original input and results, without sending new requests to the models.

Restoring a session is different from rerunning an analysis.

Retry

Retry failed or incomplete requests without necessarily restarting the entire workflow.

Manual retry limits and task-specific handling are used for Analyze, Compare, and Judge operations.

Copy and Export

- Copy results in Markdown format.
- Copy simplified plain-text versions.
- Export individual sessions as JSON.
- Export the complete history as JSON.

Request and Cost Management

The application includes internal mechanisms for:

- Managing concurrent requests.
- Handling model concurrency limits and waiting states.
- Coordinating request execution.
- Prioritizing models based on estimated cost.
- Handling cancellations and certain retry conditions.
- Tracking response times and execution status.

These mechanisms help manage the practical complexity of running multiple model requests within one application.

---

What Makes It Different?

A conventional multi-model comparison tool primarily collects and displays different answers.

Scientific Logic Auditor adds structured reasoning analysis and an optional evaluation stage.

Aspect| Basic Multi-Model Comparison| Scientific Logic Auditor
Input processing| Submit the same prompt to multiple models| Use dedicated instructions for structured reasoning analysis
Analysis| Display generated answers| Examine claims, evidence, assumptions, and logical consistency
Comparison| Compare final responses| Inspect differences across structured analyses
Evaluation| Primarily left to the user| Optional evaluation by a separate Judge model
Input isolation| Depends on the prompt| Explicitly separates submitted content from application instructions
Session management| Varies by tool| History, Restore, Retry, Copy, and Export

The central distinction is the focus on the reasoning behind conclusions, not just the conclusions themselves.

Two models may reach the same answer while relying on different assumptions, overlooking different evidence, or making different logical errors. Their agreement alone does not establish that either analysis is sound.

Scientific Logic Auditor is designed to make those differences easier to examine.

---

Evaluation Scope and Limitations

The project focuses on evaluating the quality of model-generated analyses, but several limitations remain important.

- The AI Judge is itself an LLM and can produce incorrect or poorly justified evaluations.
- A separate Judge model does not automatically provide independent verification.
- The application does not currently establish ground truth for every factual claim.
- Judge evaluations are qualitative; the application does not provide a validated numerical accuracy benchmark or guarantee an objectively correct ranking of models.
- Prompt-level input isolation is not a guarantee against all prompt injection attacks.
- Analysis quality depends partly on the selected models, their capabilities, and the information available to them.

The reliability of the Judge and the consistency of its evaluations remain important areas for further testing.

---

Target Use Cases

- AI Developers: Examine and compare the reasoning produced by different LLMs.
- SaaS Founders and AI Product Builders: Investigate the quality and limitations of model-generated outputs used in AI-powered products.
- AI Researchers: Explore differences in reasoning behavior and model evaluation.
- Prompt Engineers: Examine how different models interpret and analyze the same input.
- Critical Thinkers and Analysts: Investigate unsupported claims, hidden assumptions, weak arguments, and unjustified conclusions.

---

Development Status

Current Stage: Functional Private Version — Pre-Release

The core application workflows are functional and have been tested locally.

The application has not yet been opened for public use. Work is currently focused on remaining fixes, security improvements, and final checks before public release.

Roadmap

- [x] Core Analyze, Compare, and Judge workflows.
- [x] Result handling and execution management.
- [x] History, Restore, Retry, and Export.
- [ ] Remaining fixes and security improvements.
- [ ] Final testing and pre-release validation.
- [ ] Public release.

The Judge's reliability is a separate ongoing evaluation challenge and should not be confused with completion of the application's core functionality.

---

Get Involved

The project overview is currently public, while the application itself is not yet available for public use.

Feedback is welcome, particularly on:

- Challenging reasoning cases.

- Potential weaknesses in the analysis instructions.

- Judge evaluation criteria and reliability.

- Prompt injection and input-handling edge cases.

- Useful improvements to the analysis and comparison workflows.

- ⭐ Star the repository to follow project updates.

- 💬 Open an Issue to discuss evaluation cases, report concerns, or suggest improvements.

Critical feedback and technically grounded suggestions are welcome.
