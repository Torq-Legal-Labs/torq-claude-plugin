---
name: training-request
description: "Use when an employee wants to file a training request, flag a process issue or propose an improvement in Torq through its guided interview."
---

# File A Training Request

Use this skill when an employee wants to file a training request, flag a process issue, or propose an improvement. This is a GUIDED, SERVER-DRIVEN interview: the server owns the required-field checklist per lane, decides when the request is complete, and produces the finalized draft. Your job is to converse each field to a specific answer and file it — never to invent the questions or decide the request is "ready" yourself.

There are three lanes; open the interview in the one that fits:
- training: the employee wants the firm to build or run training on a topic.
- process_issue: the employee is flagging a workflow that breaks down.
- improvement_idea: the employee is proposing a change.
If it is not obvious from what they said, ask which of the three they mean before opening the interview, then pass it as requestType on the first turn.

Loop:
1. Call resume_training_request_intake first to see the durable state: the currentFieldKey (where to resume), the collected answers, the transcript, requiredSatisfied, and any existing draft. If a draft is already present, read it back and skip to confirmation.
2. Work the field the engine is collecting. Call answer_training_request_intake with the employee's message. Pass message:null on the very first turn to OPEN the interview so the coach speaks the lane opener. Relay the coach's "message" event substance faithfully — ask what the engine is asking, in your own conversational voice, but never invent a different question or skip ahead.
3. If a turn returns a "grounding" event, the firm already has training that looks related. Surface it naturally — e.g. "we already have training on X — do you still want to file this, or does that cover it?" — and let the employee decide. Do not file over their objection and do not hide the match.
4. If a turn returns a "fallback" event, the interviewer is temporarily degraded: tell the employee plainly and offer to retry, rather than pretending it was a real answer.
5. Keep looping answer_training_request_intake until a turn returns a "proposed" event carrying the finalized draft. Do not fabricate the request yourself — use exactly what "proposed" carries (the employee may refine it in another turn first).
6. Summarize the proposed request in the thread (title + what it says) and get an EXPLICIT yes. Only then call confirm_training_request_intake with accept:true to file it. Returns the created request id + status.

Determinism and safety:
7. Completion is the server's required-field check, never your judgment. confirm with accept:true is rejected with a 422 until every required field is collected — so never call it before a "proposed" draft exists and the employee has confirmed. If they want to change something first, call answer again to refine, then re-summarize.
8. Off-topic turns are fine: answer the unrelated question normally, then offer to pick the intake back up ("want to keep going on your training request?"). There is NO lockout — the interview is durable and resume_training_request_intake reopens exactly where you left off.
9. There is one interview per employee: a second start resumes the in-flight run rather than restarting it, so always resume before answering. If the employee wants to abandon a started request (e.g. after seeing an existing-training match), call cancel_training_request_intake so a fresh one can begin.

Torq tools this guide uses: `resume_training_request_intake`, `answer_training_request_intake`, `confirm_training_request_intake`, `cancel_training_request_intake`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
