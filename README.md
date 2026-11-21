# Project 9: L'Oréal Routine Builder
L’Oréal is expanding what’s possible with AI, and now your chatbot is getting smarter. This week, you’ll upgrade it into a product-aware routine builder. 

Users will be able to browse real L’Oréal brand products, select the ones they want, and generate a personalized routine using AI. They can also ask follow-up questions about their routine—just like chatting with a real advisor.
## Local preview

Open this folder in VS Code and run `python3 -m http.server 8001 --bind 127.0.0.1`. Visit http://localhost:8001.

## Connect the existing Worker

The frontend uses https://loreal-chatbot.emmanuelokwuma111.workers.dev/ and sends selected product records plus conversation history in a messages array. Replace the existing Worker's code with RESOURCE_cloudflare-worker.js to support larger product requests. Keep the existing OPENAI_API_KEY secret in Cloudflare. Set the ALLOWED_ORIGIN text variable to `https://emmanuelokwuma.github.io,http://localhost:8001` to allow both Pages and this local preview. Values are exact origins separated by commas; no trailing slashes. No secret belongs in this folder.

## Features and checks

Cards are keyboard-operable selection buttons; About this product expands a description independently. The selection list supports removal and Clear all. Only selected IDs persist in localStorage; descriptions come from products.json on each load. Search matches names, brands, categories, and descriptions alongside category filtering. Generate sends only selected product records, including their descriptions, and optional user preferences. Follow-ups retain the complete successful conversation in memory. Selection changes do not rewrite earlier routines; Generate again to use new selections. New chat clears conversation history but keeps selected products. A failed request leaves successful history unchanged and can be retried.

Verify real routine generation and follow-up answers after updating the Worker. Test saved selections on reload, keyboard selection, descriptions, no search results, narrow layouts, and a private browser. The starter dataset supplies product information; it is not a live inventory feed. The optional web-search checkbox uses gpt-5-search-api through the Worker and displays clickable inline citations and a source list. Ordinary routines use gpt-4.1 without web search. Search failures preserve the draft for retry; answers without citations are marked as having no sources returned. The Language selector switches English/LTR and Arabic/RTL, translating controls and mirroring the grid, selection list, and conversation. Product catalog names and descriptions retain their supplied language. Language preference persists on this device. Arabic mode requests Arabic AI replies. Update the Worker before testing search; the frontend detects older Worker versions. Verify search with a current product question and open its source links; switch languages and check selections remain intact.
