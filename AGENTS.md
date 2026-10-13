# Local model runtime development

- GPU execution requires explicit user approval for the particular action. Approval to implement, test, or debug code does not authorize GPU execution.
- Until approval is given, do not run models, download weights, start model servers or GPU containers, start Docker/WSL services that might load models, or invoke GPU diagnostic/probing tools. Halt and ask before a required GPU step.
- Use CPU-only synthetic tests and offline contract fixtures while approval is pending. Do not silently substitute cloud inference.
- Keep document extraction, indexing, citations, and source-folder access in the Local RAG repository.
