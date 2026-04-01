# Branch `dsv32-opt`

DSv32-related aiter work for ROCm, published from this fork:  
**[frida-andersson/aiter](https://github.com/frida-andersson/aiter)**.

## Provenance

| Layer | Source | Notes |
|--------|--------|--------|
| **Base** | [maeehart/aiter](https://github.com/maeehart/aiter) branch `maeehart/fix-fmoe-1stage-gfx950` | Forked at [`f583a5d`](https://github.com/frida-andersson/aiter/commit/f583a5d53665d39933350ada1e3cdce38a879966) (gfx950 `get_2stage_cfgs` workaround). **This branch reverts that heuristic** — the decode HIP issues are addressed by `ck_moe_stage1` split-K scratch ([ROCm/aiter#2547](https://github.com/ROCm/aiter/pull/2547)) instead of forcing 1-stage on gfx950. |
| **moe_buf** | Fork | Optional pre-allocated `moe_buf` in `moe_sorting` / `fused_moe` for vLLM integration (reduces `__amd_rocclr_copyBuffer` traffic in profiling) |
| **ck_moe_stage1** | [ROCm/aiter#2547](https://github.com/ROCm/aiter/pull/2547) | Split-K scratch buffer sizing aligned with CK `sorted_size` / scatter padding |

## vLLM

Uses matching plumbing in vLLM (`moe_buf` threaded through `rocm_aiter_fused_moe` / `_aiter_ops`).
