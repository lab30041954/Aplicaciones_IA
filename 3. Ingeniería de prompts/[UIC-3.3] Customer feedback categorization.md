# [UIC-3.3] Customer feedback categorization

---

## Input

Analyze this customer feedback and categorize the issues. Use these categories: UI/UX, Performance, Feature Request, Integration, Pricing, and Other. Also rate the sentiment (Positive/Neutral/Negative) and priority (High/Medium/Low).

Here is the feedback: The new dashboard is a mess! It takes forever to load, and I can't find the export button. Fix this ASAP! 

## Output (Gemini 3 Fast)

Ouch. That's some spicy feedback, but honestly? It's exactly the kind of direct input that helps a product team figure out where the "fire" is.

Here is the breakdown of that user's frustration:

#### **Feedback Analysis**

| Metric | Rating |
| --- | --- |
| **Sentiment** | **Negative** (Frustrated, urgent tone) |
| **Priority** | **High** (Impacts core usability and speed) |

#### **Issue Categorization**

* **UI/UX**
* *"The new dashboard is a mess!"* --- General layout/organization issues.
* *"I can't find the export button."* --- Discoverability and navigation friction.


* **Performance**
* *"It takes forever to load."* --- Latency or optimization problems.

#### **Summary of Key Pain Points**

The user is experiencing a "double whammy": they are frustrated by the visual layout changes (UI/UX) and further aggravated by technical slowness (Performance). The inability to find a core function like "Export" suggests that the recent update may have buried essential tools.

Would you like me to draft a professional, empathetic response to this customer that acknowledges their frustration and provides a timeline for a fix?

---

## Input

Our CS team is overwhelmed with unstructured feedback. Your task is to analyze feedback and categorize issues for our product and engineering teams. Use these categories: UI/UX, Performance, Feature Request, Integration, Pricing, and Other. Also rate the sentiment (Positive/Neutral/Negative) and priority (High/Medium/Low). Use JSON format in your response, as in the following example:

```
<example>
Feedback: The new dashboard is a mess! It takes forever to load, and I cant find the export button. Fix this ASAP!
{
    "feedback": "The new dashboard is a mess! It takes forever to load, and I cant find the export button. Fix this ASAP!",
    "category": "UI/UX",
    "sentiment": "Negative",
    "priority": "High"
}
</example>
```

Feedback: Your pricing is ridiculous! $99/mo for basic features? I'm switching to a competitor.

## Output (Gemini 3 Fast)

```
json
{
    "feedback": "Your pricing is ridiculous! $99/mo for basic features? I'm switching to a competitor.",
    "category": "Pricing",
    "sentiment": "Negative",
    "priority": "High"
}
```

