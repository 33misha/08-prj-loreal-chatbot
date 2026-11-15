# Project 8 submission preparation

These drafts use the project’s implementation and your comments about the experience. Read and personalize them before putting them in your assignment document. Keep only statements that describe your own experience. The frontend is published; successful live AI behavior still needs verification before submission.

## 1. Live project URL

**Published project URL:** [https://33misha.github.io/08-prj-loreal-chatbot/](https://33misha.github.io/08-prj-loreal-chatbot/)

The page and its current versioned CSS/JavaScript assets returned HTTP 200 on November 14, 2026. The Worker currently returns HTTP 500 because its server-side secret is missing. The class administrator must restore that configuration before real replies, relevance, and memory can be verified. Test the finished site in a private browser after the final review changes are published.

## 1B. LevelUps implemented

- **Conversation history — 10 bonus points:** Follow-up requests include recent conversation messages so the assistant can use previous context. Confirm that it remembers a name or preference during live testing.
- **Display user question above response — 5 bonus points:** A dedicated latest-question panel shows the current question and updates on the next submission.
- **Chat conversation UI — 10 bonus points:** User and assistant messages have distinct bubbles and labels in a readable conversation layout.

## 2. Reflection: building an AI-powered chatbot — 10 points

**Draft based on your experience; review before submitting:**

The most challenging part for me was connecting the Cloudflare Worker to the API. There were several pieces that needed to work together: the chat form had to collect a question, JavaScript had to send it in the right format, and the Worker had to communicate with the AI service. Seeing how the different digital tools connected was the most interesting part of the project.

To investigate the connection, I checked the Worker’s metrics, and the project connection was tested separately from the page layout. The website now loads online and sends questions to the Worker. During the November 14 review, the Worker reported that its server-side configuration was missing. The class administrator still needs to restore that configuration before a successful AI reply can be verified. This helped me understand why it is useful to check each connection separately and why an online interface and an available external service both matter.

**Review before submitting:** Confirm that this describes your own involvement, explain one troubleshooting step in your own words, and update the outcome once the administrator restores the service. Do not claim that the connection or AI answers were fully fixed until you have tested them successfully.

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

- [ ] Have the class administrator restore the deployed Worker’s missing `OPENAI_API_KEY` secret and verify its configuration; do not add a key to the frontend.
- [ ] Recheck the live response after configuration is restored. Earlier exhausted-credit errors may need separate administrator action if they return.
- [ ] Confirm the live Worker returns an actual assistant reply.
- [ ] Verify relevant answers and polite refusal of unrelated questions.
- [ ] Verify conversation memory with a follow-up question.
- [x] Check the logo, latest-question panel, and distinct chat bubbles locally in Chrome.
- [x] Pass all 35 November 14 local Chrome checks, including desktop/mobile layouts, keyboard navigation, script-failure fallback, incomplete answers, and error recovery with simulated Worker replies.
- [ ] Repeat the browser checks on the published site with the live service restored.
- [ ] Confirm the deployed Worker uses the required model and keeps its key as a Worker secret; ask the class administrator if needed.
- [x] Commit and push the original implementation and cache-refresh fix.
- [x] Publish the frontend with GitHub Pages and confirm that the public page and versioned assets are reachable.
- [ ] Open the published site in a private browser and confirm that the latest review fixes load (asset version `20261114-1`).
- [ ] Review all three reflection drafts for personal accuracy and update the final troubleshooting outcome.
- [ ] Copy the URL, LevelUps, and reflections into the assignment document.
- [ ] Export the completed assignment document as a PDF and upload it to HQ.

The rubric includes **80 required points and 25 optional bonus points, for 105 possible points**. This document prepares the written work; it does not claim that a score has been awarded.
