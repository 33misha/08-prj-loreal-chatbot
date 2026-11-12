# Project 8 submission preparation

These drafts use the project’s implementation and your comments about the experience. Read and personalize them before putting them in your assignment document. Keep only statements that describe your own experience. Live AI behavior and publication must be verified before submission.

## 1. Live project URL

Paste the verified GitHub Pages URL here: **[Add your working published URL]**

The expected address for this repository is `https://33misha.github.io/08-prj-loreal-chatbot/`. It returned HTTP 404 during the current check. Confirm it actually loads the finished project in a private browser before submitting it.

## 1B. LevelUps implemented

- **Conversation history — 10 bonus points:** Follow-up requests include recent conversation messages so the assistant can use previous context. Confirm that it remembers a name or preference during live testing.
- **Display user question above response — 5 bonus points:** A dedicated latest-question panel shows the current question and updates on the next submission.
- **Chat conversation UI — 10 bonus points:** User and assistant messages have distinct bubbles and labels in a readable conversation layout.

## 2. Reflection: building an AI-powered chatbot — 10 points

**Draft based on your experience; review before submitting:**

The most challenging part for me was connecting the Cloudflare Worker to the API. There were several pieces that needed to work together: the chat form had to collect a question, JavaScript had to send it in the right format, and the Worker had to communicate with the AI service. Seeing how the different digital tools connected was the most interesting part of the project.

The project helped me understand why it is useful to check each connection separately. For example, a live test reached the Worker but returned an error saying that the service had no credits remaining. The frontend can explain that problem to the user, but the Worker owner still needs to resolve it before successful AI replies can be tested. I learned that a working interface and a working external service both matter when building an AI-powered application.

**Personalize if needed:** Add one troubleshooting step you personally tried. If the service-credit problem has been resolved, describe the actual resolution rather than leaving the unfinished status above.

## 3. Reflection: interview and networking talking points — 10 points

**Draft talking points to adapt to your own contribution:**

- “This project is a beauty assistant that helps people explore L’Oréal products and routines through a chat interface.”
- “It uses plain JavaScript to send asynchronous requests and display responses. Follow-up questions include conversation history so the assistant can use earlier preferences.”
- “The frontend calls a Cloudflare Worker, which keeps the API credential out of publicly served browser files.”
- “The interface includes responsive layouts, clear message labels, loading feedback, and error recovery. Those details help make an API-based feature usable.”
- “The most challenging part for me was connecting the Worker to the API. It was interesting to see how the different tools connected into one application.”

**Personalize:** Describe the parts you implemented or understand best. Be ready to explain how the request travels from the form to the Worker and back. Mention any help or tools used accurately if asked.

## 4. Reflection: presenting to a L’Oréal recruiter — 10 points

**Draft to review and personalize:**

I would highlight how the chatbot combines a recognizable L’Oréal visual identity with a practical product-discovery experience. The provided logo, restrained black-and-white design, clear typography, and separate message bubbles make the assistant easy to recognize and use. Its instructions focus on L’Oréal products and routines, and it can ask follow-up questions to understand a user’s needs.

On the technical side, the project demonstrates asynchronous JavaScript, conversation state, safe text rendering, and communication through a Cloudflare Worker. The loading and error states show attention to what happens when a service is slow or unavailable. I would explain the project as a student prototype and be clear about which features have been tested successfully and which need further work.

**Personalize:** Add one design choice you made, one example conversation you actually tested, and one improvement you would make next. Do not claim official affiliation with L’Oréal or guaranteed product accuracy.

## Final submission checklist

- [ ] Have the Worker owner resolve `credit_balance_exhausted`; waiting or retrying cannot restore exhausted service credits.
- [ ] Confirm the live Worker returns an actual assistant reply.
- [ ] Verify relevant answers and polite refusal of unrelated questions.
- [ ] Verify conversation memory with a follow-up question.
- [x] Check the logo, latest-question panel, and distinct chat bubbles locally in Chrome.
- [x] Test desktop, mobile widths, keyboard navigation, and error recovery with simulated Worker replies.
- [ ] Repeat the browser checks on the published site with the live service restored.
- [ ] Confirm the deployed Worker uses the required model and keeps its key as a Worker secret; ask the class administrator if needed.
- [ ] Commit and push the completed files.
- [ ] Publish the frontend with GitHub Pages and test the public URL in a private browser.
- [ ] Replace the URL placeholder and review all three reflection answers.
- [ ] Copy the URL, LevelUps, and reflections into the assignment document.
- [ ] Export the completed assignment document as a PDF and upload it to HQ.

The rubric includes **80 required points and 25 optional bonus points, for 105 possible points**. This document prepares the written work; it does not claim that a score has been awarded.
