---
name: mymemory-translate
description: Translate text using the MyMemory free API. Use when the user asks for translation (e.g., "翻译", "translate", "中译英", "英译中", "翻成中文/英文/日文") or requests language conversion/bilingual output. Default langpair is en|zh unless the user specifies otherwise.
---

# MyMemory Translate

1. Detect translation intent and extract the source text.
   - If source text is missing, ask for it first.
   - Use `langpair=en|zh` by default.

2. Resolve `langpair`.
   - If user specifies both source and target languages, use them directly.
   - If user specifies only one side, infer the other side when clear; otherwise ask one concise clarifying question.
   - Accept ISO/RFC3066 language codes (for example: `en`, `zh`, `zh-CN`, `ja`, `ko`, `fr`, `de`, `es`, `ru`).
   - Map common Chinese language names when needed: 中文→`zh`, 英文→`en`, 日文→`ja`, 韩文→`ko`.

3. Call the API with URL-encoded parameters.
   - Endpoint: `https://api.mymemory.translated.net/get`
   - Required parameters:
     - `q=<text>`
     - `langpair=<source>|<target>`
     - `de=feihong0808_test@2925.com`
   - Example:
     ```bash
     curl --get 'https://api.mymemory.translated.net/get' \
       --data-urlencode "q=<TEXT>" \
       --data-urlencode "langpair=<SRC>|<TGT>" \
       --data-urlencode 'de=feihong0808_test@2925.com'
     ```

4. Parse response JSON and use `responseData.translatedText` as the final translation.

5. Return concise output.
   - Primary format: `译文：<translatedText>`
   - Add `语言对：<SRC>|<TGT>` only when useful (for example, non-default pair or user asks).

6. Handle errors gracefully.
   - If API fails or translation is empty, return a short error and ask user to retry.
   - For long text, split by sentence/newline and translate in chunks.
