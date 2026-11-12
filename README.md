# Project 8: L’Oréal Beauty Assistant

A student chatbot for exploring L’Oréal products and personalized skincare, makeup, haircare, and fragrance routines. The frontend uses HTML, CSS, and plain JavaScript. It is a learning project, not an official L’Oréal service.

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

The Worker holds the OpenAI API key as a Cloudflare secret. Students do not need a key. **Never add API keys or secrets files to this repository.** If the assignment PDF gives different key-handling instructions, use the class-hosted Worker approach documented here and in `AGENTS.md`.

`RESOURCE_cloudflare-worker.js` is server-side reference code for the class administrator. It is not loaded by `index.html`. The reference uses `gpt-4.1`, validates requests, adds L’Oréal topic instructions, and preserves HTTP error statuses. Editing the reference file does **not** update the deployed Worker; the administrator must deploy it separately. See the [Chat Completions documentation](https://developers.openai.com/api/reference/resources/chat/subresources/completions/methods/create) for the request format.

The latest live diagnostic returned **HTTP 429**, with error type `insufficient_quota` and code `credit_balance_exhausted`. The deployed Worker wraps the provider response in a JSON string in its `details` field; the frontend reads that nested error as well as ordinary error objects. The service reported that no credits remain. The Worker owner must resolve the service’s exhausted credits; waiting or repeatedly retrying does not restore them. Browser preflight permissions were accepted, so that check did not identify a CORS failure. The frontend shows a clear availability message. See the [OpenAI error-code documentation](https://developers.openai.com/api/docs/guides/error-codes) for the distinction between request-rate and quota errors.

## Features and conversation behavior

- The provided L’Oréal logo and a black-and-white interface identify the project theme.
- System instructions keep the assistant focused on L’Oréal products and routines.
- User and assistant messages appear in distinct chat bubbles.
- The latest question is highlighted above the conversation and changes on each submission.
- Follow-up requests include recent conversation history to preserve context. The frontend limits the amount of history sent, so very old details can leave the request context during a long conversation.
- History is kept in browser memory for the current page session. It is not saved to browser storage, and refreshing the page or starting a new chat clears it. Messages are sent to the Worker to generate replies.
- Loading feedback, duplicate-submission protection, a 30-second request timeout, and recoverable errors keep the form usable.
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

Local simulated checks can verify frontend behavior without a paid AI request. They do not establish that the live Worker or the AI’s answers are working. The successful-answer, relevance, and memory checks remain pending until the Worker’s service credits are restored.

## Checks completed on November 12, 2026

- All 26 local Chrome browser checks passed using simulated Worker replies. Checks covered the logo, 320px/375px/1440px layouts, message bubbles, latest question, keyboard submission, follow-up request history, New chat, input limits, safe text rendering, and recovery from failed or stalled requests.
- A long-conversation check confirmed that outgoing requests retain complete recent exchanges and remain within the Worker’s message limit.
- No uncaught JavaScript exceptions were detected during these browser checks.
- Worker reference checks passed for request validation, the required model, server instructions, error status handling, and CORS headers.
- Live Worker preflight access passed. The live AI request failed with exhausted credits, and the expected GitHub Pages address returned 404.

## Publish with GitHub Pages

1. Commit and push the finished project to your GitHub repository.
2. Open the repository’s **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and **/(root)**, then save.
4. Wait for GitHub Pages to finish publishing and copy the URL shown there.
5. Open that URL in a private browser and repeat the live chat and mobile checks.

These steps follow the [GitHub Pages publishing-source documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

Based on this repository’s origin, the expected address is:

```text
https://33misha.github.io/08-prj-loreal-chatbot/
```

The address returned HTTP 404 during the current deployment check, so publication still needs to be completed or corrected. Submit the working **GitHub Pages link**, rather than the repository, Codespace, or Worker URL.

See `SUBMISSION.md` for reflection drafts, the LevelUp list, and the final submission checklist.
