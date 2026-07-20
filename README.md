# ecm-avaliacoes
Final project for the Building AI course

## Summary
An AI-powered system that automatically evaluates the quality of customer service interactions handled by staff at ECM (Escritório Contábil Madruga), an accounting firm, by analyzing WhatsApp Business conversations with an LLM (GPT-4o) and generating scores and structured feedback.

## Background
Accounting firms handle a high daily volume of customer service interactions over WhatsApp, spread across multiple departments and employees. Manually reviewing the quality of every conversation is not feasible at scale, and service issues usually only surface after a customer has already complained.

* Managers can't manually read every conversation to check service quality
* Poor service quality is often discovered only after a customer complaint or churn
* No consistent, objective way to compare service quality across employees and departments

This is a recurring, high-frequency problem: every single customer interaction is a potential quality issue. My personal motivation came from having recently structured and gotten approval for WhatsApp Business message templates across every department of the firm (Accounting, Tax, HR, Legal Registration, Finance, Front Desk) — that process made it clear that standardizing *how* the firm communicates isn't enough; it's also necessary to *measure* the quality of what's actually being delivered to the customer. This topic matters because it sits at the intersection of a real, everyday business problem and a very concrete, measurable AI application.

## How is it used?
The system runs in the background as part of the firm's existing WhatsApp workflow. Conversations are handled normally by employees through Digisac (the firm's WhatsApp Business platform); after an interaction, the system pulls the conversation, sends it to an LLM for evaluation, and stores the resulting score and feedback.

Management reviews the evaluations periodically to spot employees or departments whose service quality is dropping, and uses the feedback to guide coaching rather than punishment. The main users are:

* **Managers / partners**, who review evaluation reports and identify patterns needing attention
* **Employees**, whose conversations are evaluated — the tool is meant to support their development, not to punish them, since a purely punitive framing risks harming morale
* **Clients of the firm**, who benefit indirectly from improved service quality

## Data sources and AI methods
Conversation data comes from the firm's own WhatsApp Business account, extracted through its integration with [Digisac](https://digisac.com.br/), the platform used to manage customer conversations across all departments.

The evaluation itself is done with an LLM (GPT-4o) used as a judge: each conversation is sent with a structured prompt defining the evaluation criteria (clarity, response time, courtesy, issue resolution, adherence to department protocol), and the model returns a score per criterion plus written feedback. No custom model is trained — the approach relies entirely on the LLM's language understanding, applied consistently across every conversation.

| Data | Description |
| ----------- | ----------- |
| Source | WhatsApp Business conversations via Digisac |
| Volume | All conversations across 6 departments (Accounting, Tax, HR, Legal Registration, Finance, Front Desk) |
| AI method | LLM-as-judge evaluation (GPT-4o) with a structured scoring prompt |

## Challenges
* The model evaluates written text only — tone of voice and emotional nuance that don't come through in writing can be misread
* LLM evaluations can be inconsistent or biased between runs; scores should be periodically checked against a manually reviewed sample
* The system lacks full business context: e.g. a firmer response to a delinquent client shouldn't automatically be scored as "poor service"
* It depends entirely on the reliability of the Digisac data integration
* Ethically, using AI to evaluate employee performance requires transparency with staff and safeguards against the tool being used punitively rather than developmentally

## What next?
* A consolidated dashboard with score history per employee and per department
* Automatic alerts for interactions flagged as critical (e.g. dissatisfied customer, very slow response)
* Cross-referencing evaluation scores with customer satisfaction data (e.g. NPS) to validate that the AI's scoring actually reflects customer perception
* Extending evaluation to other service channels beyond WhatsApp

To move forward, I'd benefit from more experience in prompt evaluation/validation techniques (to make the LLM-as-judge scoring more consistent) and from feedback on how to present performance data to employees in a way that supports growth rather than creating anxiety.

## Acknowledgments
* Built on top of [Digisac](https://digisac.com.br/), the WhatsApp Business platform used by ECM (Escritório Contábil Madruga)
* Evaluation powered by OpenAI's GPT-4o via the [OpenAI API](https://platform.openai.com/docs)
* Inspired by the real, day-to-day challenge of ensuring consistent service quality across a growing accounting firm
