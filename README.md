# GPU Optimization for AI-ML Systems · Free Live Sessions

Make AI models faster and cheaper to run, and prove it with numbers.

**Free · Live · 30 minutes · Mondays and Thursdays, 7:30 PM Central** · with Emmanuel N. ([Transformed 2 Succeed](https://transformed2succeed.com))

### [Register free on Zoom](https://us06web.zoom.us/meeting/register/fT235rLjQaihJYrWj2_vjw)

Register once and you're in for every session. Zoom emails you the join link and reminders. Bring your questions: every session ends with live Q&A.

## Watch the recordings

Missed a session or want to watch it again? Recordings are added here after each live session.

| Date | Recording |
|---|---|
| _Coming after the first session_ | |

## Set up your lab (do this before you join)

Want to code along? Follow **[SETUP.md](SETUP.md)**. It takes about 15 minutes, once, and works on any computer (or right in your browser with GitHub Codespaces).

## Downloads

Everything you need is in the [`downloads`](downloads) folder:

| File | What it is |
|---|---|
| [06_GPU_Optimization_for_AI_ML_Systems_Free_Live_Session.pdf](downloads/06_GPU_Optimization_for_AI_ML_Systems_Free_Live_Session.pdf) | The session slides (PDF) |
| [06_GPU_Optimization_for_AI_ML_Systems_SETUP_GUIDE.pdf](downloads/06_GPU_Optimization_for_AI_ML_Systems_SETUP_GUIDE.pdf) | The setup guide (PDF version of SETUP.md) |
| [gpu-ai-optimization-labs.zip](downloads/gpu-ai-optimization-labs.zip) | The lab files (unzip, then follow SETUP.md) |


## What you'll learn

1. **Measure Before You Optimize**: Cost per 1M tokens, compute vs memory-bound, and a before-and-after you can prove.
2. **Shrink the Model**: Quantize, distill, prune and route, with quality measured on your own eval set.
3. **Serve It Smarter**: KV cache math, paged attention and continuous batching: more users per GPU.

## Three things to remember

- **Measure before you optimize**: Cost per 1M tokens, the real bottleneck, and one change, re-measured.
- **Shrink the model, not the quality**: Per-channel quantization, distill, prune, route. Always a quality number.
- **Serve it smarter**: Size the KV cache, page it, batch continuously: 3x capacity, same GPU.

## Try it yourself

To get the lab files, download **[gpu-ai-optimization-labs.zip](downloads/gpu-ai-optimization-labs.zip)** from the downloads folder (see [SETUP.md](SETUP.md)).

**Module 1 · Measure Before You Optimize**: Compute-bound or memory-bound?

```bash
python3 bottleneck.py --params 8e9 --precision fp16 --gpu L4
python3 bottleneck.py --params 8e9 --precision int8 --gpu L4
```

**Module 2 · Shrink the Model**: Turn the precision dial

```bash
python3 data/make_data.py
python3 quantize.py
```

**Module 3 · Serve It Smarter**: How many users fit on one GPU?

```bash
python3 kv_calc.py --model llama-3-8b --context 8192 --users 32
python3 kv_calc.py --compare --gpu A100-80GB --context 4096
```

## All free live sessions

A different course every session. The rotation repeats every 4 weeks, so if you miss one, it comes back around.

| Week | Day | Course |
|---|---|---|
| Week 1 | Monday | [Linux for AI-ML Systems](https://github.com/Here2ServeU/live-linux-for-ai-ml) |
| Week 1 | Thursday | [Python for AI-ML](https://github.com/Here2ServeU/live-python-for-ai-ml) |
| Week 2 | Monday | [Zero to AI-ML Systems Engineering](https://github.com/Here2ServeU/live-zero-to-ai-ml) |
| Week 2 | Thursday | [DevOps for AI-ML Systems](https://github.com/Here2ServeU/live-devops-for-ai-ml) |
| Week 3 | Monday | [SRE for AI-ML Systems](https://github.com/Here2ServeU/live-sre-for-ai-ml) |
| Week 3 | Thursday | **GPU Optimization for AI-ML Systems** (you are here) |
| Week 4 | Monday | [FinOps for AI-ML Systems](https://github.com/Here2ServeU/live-finops-for-ai-ml) |
| Week 4 | Thursday | [AI Agent Operations](https://github.com/Here2ServeU/live-ai-agent-operations) |

## Want the full course?

The membership gives you **all 8 courses, every module and every lab, for $49/month**, plus a live session every month where we build something together.

**[Join at transformed2succeed.com](https://transformed2succeed.com)**
