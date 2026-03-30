---
layout: page
permalink: /_paper/
title: Burmese-Coder-4B
description: Fine-Tuning a Small Language Model for Burmese Coding with Language-Aware Evaluation
nav: true
nav_order: 1
---

<!-- _pages/paper.md -->

<div class="post">
  <header class="post-header">
    <h1 class="post-title">Burmese-Coder-4B</h1>
    <p class="post-description">Fine-Tuning a Small Language Model for Burmese Coding with Language-Aware Evaluation</p>
  </header>

  <article>
    <div class="publications">
      {% bibliography --query @*[id=naing2026burmesecoder] %}
    </div>

    <div class="abstract">
      <h3>Abstract</h3>
      <p>
        Low-resource code generation remains underexplored, with existing benchmarks largely focused on English. Burmese coding presents a dual challenge: generating correct programs while maintaining natural Burmese explanations without corrupting programming syntax. In practice, models frequently exhibit mixed-script hallucination, unstable terminology, and cross-language token drift despite producing functionally correct code. 
      </p>
      <p>
        We introduce <strong>Burmese-Coder-4B</strong>, a Burmese coding assistant adapted from the Gemma-3 4B family via supervised fine-tuning and Direct Preference Optimization (DPO). The alignment stage incorporates a language-aware penalization signal to suppress mixed-language outputs and improve linguistic consistency.
      </p>
      <p>
        Evaluation is conducted using a two-track framework combining functional correctness (Pass@1) and rubric-based <strong>LLM-as-a-Judge</strong> scoring using Gemini 2.5 and DeepSeek V3. Burmese-Coder-4B matches the base model on Pass@1 (62.0%) while improving rubric quality (3.779 vs. 3.203) and reducing mixed-language penalty (0.02 vs. 0.69). Compared to Qwen2.5-3B (45.0% Pass@1, 2.526 rubric), the burmese-coder model achieves stronger alignment in both code correctness and Burmese language quality. These results demonstrate that functional correctness alone is insufficient for evaluating low-resource coding assistants. We release the model and evaluation framework to support reproducible research.
      </p>
    </div>

    <div class="links">
      <a href="https://huggingface.co/WYNN747/burmese-coder-4b" class="btn btn-sm z-depth-1" role="button" target="_blank">Model (Hugging Face)</a>
      <a href="https://github.com/WaiYanNyeinNaing/burmese-coding-eval" class="btn btn-sm z-depth-1" role="button" target="_blank">Code (GitHub)</a>
      <a href="{{ '/assets/pdf/burmese_coder_4b.pdf' | relative_url }}" class="btn btn-sm z-depth-1" role="button" target="_blank">PDF</a>
    </div>

    <div class="pdf-viewer mt-4">
      <object data="{{ '/assets/pdf/burmese_coder_4b.pdf' | relative_url }}" type="application/pdf" width="100%" height="800px">
        <p>Your browser does not support PDFs. <a href="{{ '/assets/pdf/burmese_coder_4b.pdf' | relative_url }}">Download the PDF</a>.</p>
      </object>
    </div>
  </article>
</div>
