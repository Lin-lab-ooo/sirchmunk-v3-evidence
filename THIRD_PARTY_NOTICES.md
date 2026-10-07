# Third-party notices

This is an independent experimental extension. It is not an official ModelScope release and is not endorsed by ModelScope or the dataset authors.

## Authored extension

The existing MIT notice in [LICENSE](LICENSE) covers the authored research code and associated documentation. Retain that notice when redistributing this code. Shared adapter modules are implementation dependencies, not additional public experimental versions.

## Sirchmunk and LENS

Upstream: [modelscope/sirchmunk](https://github.com/modelscope/sirchmunk), fixed commit `b314e11fcea87cf8146b2844cf2f991208c021d9`. Upstream is licensed under Apache License 2.0. Its full source is not bundled. The verbatim fixed-commit license is retained in [licenses/Sirchmunk-APACHE-2.0.txt](licenses/Sirchmunk-APACHE-2.0.txt), SHA256 `c71d239df91726fc519c6eb72d318ec65820627232b2f796219e87dcf35d0ab4`, matching the frozen source manifest.

Local wrappers integrate with the pinned native workflow and adapt its selection and delivery behavior. They are not an unmodified upstream product. Any independently acquired upstream source retains its own notices and obligations.

Paper: Wang et al., [LENS: In-Context Search via Latent Evidence Exploration over Dynamic Raw Documents](https://arxiv.org/abs/2608.16185v2), 2026. No paper text or figures are redistributed. Evidence localization, budget stopping, reuse/update and correction are prior-work concepts; this release does not claim these concepts, hashing or caching as original inventions.

## HotpotQA

[HotpotQA](https://hotpotqa.github.io/) is by Zhilin Yang, Peng Qi, Saizheng Zhang, Yoshua Bengio, William W. Cohen, Ruslan Salakhutdinov and Christopher D. Manning (EMNLP 2018). The dataset is CC BY-SA 4.0; the reference code is Apache License 2.0, as stated in the [official repository](https://github.com/hotpotqa/hotpot#license). Wikipedia-derived content retains its applicable obligations. Raw questions, answers and paragraphs are not distributed here.

The scoring semantics follow the [official answer evaluation script](https://github.com/hotpotqa/hotpot/blob/master/hotpot_evaluate_v1.py): normalized exact match, token F1 and yes/no/noanswer handling. The compact local scorer also computes source coverage and experiment statistics. The reference-code license is retained in [licenses/HotpotQA-code-APACHE-2.0.txt](licenses/HotpotQA-code-APACHE-2.0.txt). Anonymized measurements are authored experimental results, not a replacement for the dataset license.

## Models, tools and dependencies

The native embedding is `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`, revision `e8f8c211226b894fcb81acc59f3b34ba3efd5f42`. Model weights, `rg`/`rga`, dependency caches and the native runtime are not distributed. Obtain them independently under their own licenses. Version metadata is not a complete dependency lock or a fresh-install validation.

Historical paid measurements used the third-party `deepseek-flash` API. No API implementation, credential, account record or spending authorization is provided by this repository. The model provider's own terms apply to independently made requests.
