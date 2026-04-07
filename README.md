# Local LLM Chatbot
## What This Is
A simple chatbot that answers questions from two dummy documents about "company abc" (good) and "company bad_abc" (bad). Runs locally, no API keys.

## Why The Agent Version Failed
I tried building an agent (LangChain + tools + TinyLlama). The model kept ignoring my documents and making up answers. Asked about "abc" and it talked about a TV show. Classic small model problem.

## What Actually Worked
Forcing the search. Retrieve the document first, then feed ONLY that to the LLM. No choice. Works okay with TinyLlama. Not great, but better.

## What I'd Do Differently
1. **Bigger model or API** - TinyLlama is just too dumb for agent patterns. Mistral 7B or Groq's free tier would crush this.
2. **Skip the agent** - For simple doc Q&A, agents are overkill. RAG with a forced prompt is simpler and more reliable.
3. **Lower temperature** - 0.3 was too creative. 0.1 or 0 keeps it factual.
4. **Better prompts** - "You MUST answer from this document ONLY" works better than "you can use these tools"

## How To Run This
1. Install packages (see notebook)
2. Run cells in order
3. First run downloads TinyLlama (~1GB)
4. Uncomment `chat_with_agent()` at the bottom to talk to it

## Files
- `chatbot.ipynb` - main notebook
- `chroma_db/` - vector store (created on first run)

## Known Issues
- TinyLlama still hallucinates sometimes. Just bad at following instructions.
- Slow on CPU. Like 10-20 seconds per answer.
- Don't expect GPT-4 quality. This is a $0 budget project.

## Bottom Line
Agents need smart models. Small local models need simpler patterns. Force retrieval, don't ask nicely.
