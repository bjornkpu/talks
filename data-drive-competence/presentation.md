---
tags:
  - slides
---

# Data Driven Competence
>
> Bjørn Kristian Punsvik\
> 2025-05-20

---

What do you want the next workshop to be about?

What do you want to learn more about?

What holes do you have in your knowledge base?

---

![[Data driven competence-4.png]]

---
Data pipeline
![[data-driven.excalidraw|1000]]

---
Goal

![[opportunity score graph.png|800]]

---

- **Current Skill Level:** \
Your self-assessment of how proficient you feel in a particular topic or technology.
- **Interest:** \
How interested you are in, and to be learning more about, the topic.
- **Importance:** \
How important you believe the topic is for your role and for the team's success.
- **Satisfaction:** \
Your level of satisfaction with your current knowledge and usage of the topic.

---

8 Categories with 10 questions each

80 Questions

8 Participants from the DotNET group

---

![[Data driven competence-1.png]]
Sample of the aggregated dataset

---

![[Data driven competence.png]]
Sample of the mean and std for some backend and some frontend questions

---

What do you want the next workshop to be about?

---

![[Data driven competence-3.png|900]]

![[Data driven competence-2.png|700]]

---

```python
df['Skill_Gap'] = df['Importance'] - df['Skill_Level']
df['Priority_Score'] = (
 df['Importance'] * 0.4 +
 (5 - df['Skill_Level']) * 0.4 +
 df['Interest'] * 0.2
)
df['Opportunity_Score'] = (
 df['Importance'] + (
  df['Importance'] - df['Satisfaction']
 )
)
```

---
[Group Report](http://localhost:8888/notebooks/view.ipynb)

---

[Consultant Report](http://localhost:8888/notebooks/consultant_report.ipynb)

---

![[Group vs Consultant Comparison.png]]

---

So... What **WILL** the next workshop to be about?

---

Thank you!
