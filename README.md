# Local model runtime

This repository will manage model services on an RTX 3090 using Linux containers through Docker Desktop's WSL2 backend. It supplies local embedding, reranking, and chat inference to applications such as [Local RAG](https://github.com/Haugenau20/local-rag).

## Project status

Initial integration and implementation plan. No model backend or model weights have been selected, and no runtime services are implemented yet.

- [Runtime implementation milestones](docs/implementation-plan.md)
- [Model runtime contract](../local-rag/docs/model-runtime-contract.md) in the sibling checkout

For separately located checkouts, the contract is `docs/model-runtime-contract.md` in the Local RAG repository.

## Responsibilities

Own backend configuration, model storage, GPU resource limits, startup, readiness, model loading/unloading, and shutdown. Publish inference ports on Windows loopback addresses. Provision models explicitly before offline use and provide no cloud fallback.

The document application owns extraction, indexes, retrieval, prompts, citations, and document permissions. This runtime does not mount the document folders; text arrives only through local inference requests.

## First working milestone

Verify GPU access from a container, choose an embedding backend and a generation backend, and pass the Local RAG contract tests with synthetic requests. Provide documented start, status, warm-up, unload, and stop operations. Prefer existing backend capabilities; add an adapter only where a concrete incompatibility requires one.
