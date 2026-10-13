# Local model runtime implementation milestones

Support local applications through a stable inference contract while managing a single RTX 3090. The contract is owned by the sibling [Local RAG repository](../../local-rag/docs/model-runtime-contract.md).

## Verify the execution environment

Confirm Docker Desktop is running with its WSL2 Linux engine. Verify GPU access from a supported NVIDIA test container before selecting inference images. Record versions and supported startup commands. No model workloads are started automatically as part of documenting the design.

The initial host checks on 13 October 2026 detected an NVIDIA GeForce RTX 3090 with 24,576 MiB VRAM and driver 610.74. Ubuntu and docker-desktop were installed as WSL2 distributions and stopped. Docker CLI 27.5.1 was available; the desktop-linux engine was unavailable. These observations describe the check, not a permanent host configuration.

## Select backend and model profiles

Evaluate existing local servers for the embedding, reranking, and generation contract. Test native endpoint compatibility before building adapters. Keep model selection explicit: model revision, quantization, tokenizer, input formatting, vector dimensions, context limits, and license terms.

Measure cold and warm inference, model load/unload time, peak VRAM, and useful document retrieval quality. Use synthetic fixtures. GPU memory budgeting includes model weights, context/KV caches, batch buffers, and desktop GPU use. Establish indexing and interactive profiles from measurements rather than assuming all models should stay resident.

## Package service lifecycle

Create pinned container configurations with persistent model storage and loopback-only published ports. Document start, status, warm-up, unload, and stop operations; model unloading does not necessarily stop its server process. Use explicit model downloads during setup. Normal requests must use local files and must not download or fall back to external inference.

Distinguish service liveness, model readiness, and loading failures. Keep health endpoints useful without loading a large model unnecessarily. Apply bounded request queues and measured deadlines. Verify restart behavior and resource release before adding a custom scheduler.

## Integrate and verify offline operation

Pass contract tests for embedding ordering and dimensions, configured model identities, reranking scores, chat responses, context limits, cold starts, and unavailable services. Run the Local RAG Markdown/text milestone with outbound networking blocked after dependencies and models are installed.

Keep document content and prompts out of default logs. Give users clear errors for unavailable models, queue saturation, and out-of-memory conditions. No source-document mounts, document indexing code, or RAG database access belong in the runtime services.

## Source documentation

- [Docker Desktop GPU support](https://docs.docker.com/desktop/features/gpu/)
- [Docker WSL2 filesystem guidance](https://docs.docker.com/desktop/features/wsl/best-practices/)
- [WSL networking](https://learn.microsoft.com/en-us/windows/wsl/networking)
- [llama.cpp server capabilities](https://github.com/ggml-org/llama.cpp/blob/master/tools/server/README.md)
- [Ollama model lifecycle](https://docs.ollama.com/faq)

Backend support and flags must be verified against the versions selected for the implementation.
