# Project 8: L’Oréal Beauty Assistant

A student chatbot for exploring L’Oréal products and personalized skincare, makeup, haircare, and fragrance routines. The frontend uses HTML, CSS, and plain JavaScript. It is a learning project, not an official L’Oréal service.

**Published frontend:** [Open the L’Oréal Beauty Assistant](https://33misha.github.io/08-prj-loreal-chatbot/).

## Run the frontend

1. Open this repository in VS Code or GitHub Codespaces.
2. Preview `index.html` with the Live Preview extension, or serve the project with another local web server.
3. Ask a L’Oréal product or routine question.

No package installation or build step is needed.

## Worker connection and API key security

`script.js` sends requests to the class-hosted Worker:

```text
https://loreal-chatbot.kosulinma.workers.dev
```

The request body contains a `messages` array. Successful replies are read from `data.choices[0].message.content`.

The class-hosted Worker must hold the OpenAI API key as a Cloudflare secret. Students do not need a key. **Never add API keys or secrets files to this repository.** If the assignment PDF gives different key-handling instructions, use the class-hosted Worker approach documented here and in `AGENTS.md`. The PDF also contains an apparent exposed credential; its owner should revoke it. Do not copy that credential or the PDF into the public project.

`RESOURCE_cloudflare-worker.js` is server-side reference code for the class administrator. It is not loaded by `index.html`. The reference uses `gpt-4.1`, validates requests, adds L’Oréal topic instructions, and preserves HTTP error statuses. Editing the reference file does **not** update the deployed Worker; the administrator must deploy it separately. See the [Chat Completions documentation](https://developers.openai.com/api/reference/resources/chat/subresources/completions/methods/create) for the request format.

The reference stops provider requests after 25 seconds, before the frontend’s 30-second timeout. It reads incoming request data in chunks and rejects bodies larger than 1 MiB, including requests without a `Content-Length` header. These safeguards are part of the reference code and need administrator deployment to take effect on the live Worker.

**Current live blocker — November 14, 2026:** the deployed Worker returns **HTTP 500** and reports that its `OPENAI_API_KEY` secret is not set. The class administrator must configure the deployed Worker’s server-side secret and verify the deployment. This cannot be repaired by adding a key to the frontend. The published page and its versioned CSS/JavaScript assets return HTTP 200, and the Worker response includes browser-access headers.

Earlier checks on November 12–13 returned HTTP 429 with `insufficient_quota` / `credit_balance_exhausted`. That is historical evidence, not the current failure. After the administrator restores the missing configuration, another live test must establish whether any account or service-limit problem remains. The frontend handles both ordinary service errors and the class Worker’s JSON-string `details` wrapper without displaying raw provider messages. See the [OpenAI error-code documentation](https://developers.openai.com/api/docs/guides/error-codes) for error categories.

## Features and conversation behavior

- The provided L’Oréal logo and a black-and-white interface identify the project theme.
- System instructions tell the assistant to focus on L’Oréal products and routines and politely decline unrelated requests. Actual AI behavior still needs live testing.
- User and assistant messages appear in distinct chat bubbles.
- The latest question is highlighted above the conversation and changes on each submission.
- Follow-up requests include the most recent 19 successful question-and-answer exchanges. Very old details can leave the request context during a long conversation.
- History is kept in browser memory for the current page session. It is not saved to browser storage, and refreshing the page or starting a new chat clears it. Messages are sent to the Worker to generate replies.
- Loading feedback, duplicate-submission protection, a 30-second request timeout, and recoverable errors keep the form usable.
- A static welcome remains visible if JavaScript is unavailable. Chat controls start disabled and enable only after the script initializes, so a failed script cannot submit a question into the page URL.
- Missing Worker setup produces an instructor-help message instead of exposing internal configuration details or suggesting repeated retries.
- Provider refusal text is displayed when there is no ordinary answer. Replies stopped by the service’s length limit include an incomplete-answer notice, and the user can ask the assistant to continue.
- User input and replies are displayed as plain text, so markup is not executed as HTML.

## Design sources

The provided L’Oréal logo and restrained black-and-white presentation follow the identity discussed in [Futurebrand’s L’Oréal case study](https://www.futurebrand.com/our-work/loreal). The assignment’s [Monotype L’Oréal brand review](https://hello.monotype.com/rs/800-DWE-978/images/BrandReview_LOREAL.pdf) is the typography reference. The project uses available font substitutes; it does not bundle or claim to use licensed official L’Oréal font files.

## Manual checks before submission

1. Ask a relevant question such as “What is a simple L’Oréal skincare routine?” and confirm an actual AI reply appears.
2. Start with “My name is Alex and I have dry skin.” Then ask “What name and skin type did I mention?” Confirm the reply uses the earlier context.
3. Ask an unrelated question such as “Write a Python sorting program.” Confirm the assistant politely redirects to L’Oréal products and routines.
4. Confirm that the latest-question panel changes on the next question while the conversation bubbles remain visible.
5. Start a new chat and confirm that previous messages and the latest-question panel are cleared.
6. Check the page at 320px, 375px, 768px, and desktop widths. Test keyboard focus, Enter to send, long replies, and long unbroken text.
7. Simulate a network failure in browser DevTools. Confirm an error appears, the question remains available, and another attempt is possible. A stalled request should time out and restore the form.
8. Check the browser console and Network tab for JavaScript errors and CORS failures.

Local simulated checks can verify frontend behavior without a paid AI request. They do not establish that the live Worker or the AI’s answers are working. Successful-answer, relevance, and AI-memory checks remain pending until the administrator restores the Worker’s missing configuration and a live test succeeds.

## Rubric comparison

These are implementation and verification statuses, not awarded grades. The rubric has **80 required points and 25 optional bonus points, for 105 possible points**.

| Category | Points | Evidence and remaining work |
| --- | ---: | --- |
| L’Oréal branding | 10 | Provided logo, black-and-white styling, and responsive typography are implemented. |
| Chatbot configuration | 20 | System instructions, input capture, Worker request, and response rendering are implemented; successful live replies remain blocked. |
| AI relevance | 10 | Client and Worker-reference instructions decline unrelated requests; actual refusal behavior must be tested live. |
| Secure deployment | 10 | Frontend calls the class Worker without a key; the administrator must restore its missing secret and verify the deployed model/configuration. |
| Conversation history | 10 bonus | Follow-up requests include recent successful exchanges; request contents can be checked locally, and real AI recall remains pending. |
| Latest question above response | 5 bonus | Latest-question panel updates each submission; earlier chat bubbles remain in the conversation. |
| Chat conversation UI | 10 bonus | User and assistant bubbles have distinct appearance and speaker labels. |
| Building-chatbot reflection | 10 | Draft uses the student’s confirmed challenge and interest; review the description of personal troubleshooting. |
| Networking talking points | 10 | Draft explains the project, its architecture, and usability features; review for personal accuracy. |
| L’Oréal recruiter reflection | 10 | Draft connects brand presentation, product discovery, and technical work; review before submission. |

## Verification record

**November 14, 2026:** the published site and its current versioned assets return HTTP 200. The live Worker returns HTTP 500 for missing server-side configuration, so no successful live AI answers, refusals, or recall are claimed. The review also identified and corrected stale publication/checklist information. Local browser and Worker-reference checks are recorded separately from live service results.

- All **35 local Chrome browser checks passed using simulated API replies**. The earlier 26 checks were rerun, covering successful reply display, follow-up request history, New chat, the latest-question panel, keyboard sending, safe text rendering, input limits, mobile layouts, and recovery from network/service errors and timeouts.
- Nine additional checks covered a blocked/missing/disabled script with safe static content and no question in the URL, enabling controls after startup, the current missing-configuration response and `not_configured` errors, refusal-only responses, incomplete-answer notices, and continuation context.
- Browser replies were simulated. These results do not establish that the live service answers relevant questions correctly or remembers prior details.
- All **38 Worker-reference regression checks passed** against the final code, using native requests and simulated provider replies. They covered input validation, streaming size limits and cancellation, UTF-8 text, server-side instructions, missing configuration, reply/refusal validation, error privacy, status preservation, and fetch/body timeouts. These checks do not deploy or verify the live Worker.
- After any deployment, check the public page in a private browser and confirm that `index.html` requests the expected versioned assets. This review uses asset version `20261114-1`.

**November 12, 2026 — earlier local checks:**

- All 26 local Chrome browser checks passed using simulated Worker replies. Checks covered the logo, 320px/375px/1440px layouts, message bubbles, latest question, keyboard submission, follow-up request history, New chat, input limits, safe text rendering, and recovery from failed or stalled requests.
- A long-conversation check confirmed that outgoing requests retain complete recent exchanges and remain within the Worker’s message limit.
- No uncaught JavaScript exceptions were detected during these browser checks.
- Worker reference checks passed for request validation, the required model, server instructions, error status handling, and CORS headers.
- At that time, live Worker preflight access passed, the live AI request failed with exhausted credits, and the site had not yet been published. Publication subsequently succeeded; see the November 14 status above.

## Update the published GitHub Pages site

1. Commit and push the finished project to your GitHub repository.
2. Open the repository’s **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and **/(root)**, then save.
4. Wait for GitHub Pages to finish publishing and copy the URL shown there.
5. Open that URL in a private browser and repeat the live chat and mobile checks.

These steps follow the [GitHub Pages publishing-source documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

The published address is:

```text
https://33misha.github.io/08-prj-loreal-chatbot/
```

The published frontend returned HTTP 200 on November 14. After pushing any new review fixes, wait for Pages to deploy them and test the public page again in a private browser. When changing CSS or JavaScript, update their version query strings in `index.html` so visitors download the new assets. Submit the **GitHub Pages link**, rather than the repository, Codespace, or Worker URL.

See `SUBMISSION.md` for reflection drafts, the LevelUp list, and the final submission checklist.
