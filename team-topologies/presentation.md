---
margin: 0
theme: consult
highlightTheme: monokai
defaultTemplate: "[[q&a]]"
transition: none
tags:
  - slides
---

# Team Topology

## – Insights and Improvements

_Exploring modern team dynamics theory in light of practical experiences at Equinor.\
How to optimize team collaboration and delivery through improved structure and interaction._  
> Bjørn Kristian Punsvik\
> 2025-06-03

note:

- Welcome the audience.
- Briefly outline the purpose of the talk.
- Encourage the audience to scan the QR Code.

<https://app.sli.do/event/72o4cXe2pHoozUxvSMixJu>

---

::: title

# Challenges in Team Structures

:::

<split even wrap="2">
> [!error] **Misalignment of Teams**
> Silos lead to inefficiencies.

> [!warning] **Complexity in Structures**
> Difficulty in adapting to changing needs.

> [!tip] **Ineffective Communication**
> Hinders collaboration.

> [!info] **Lack of Clarity in Roles**
> Causes confusion and overlap.
</split>

note:

- Briefly explain why these challenges impede optimal team performance in modern organizations.
- Relate the challenges back to your own experience or anecdotes.

---
::: title

# Bjørn Kristian Punsvik

:::

<split even gap="1" no-margin>
![[profile-picture.jpg|400]]

```yaml
bk@tietoevry:~$ whoami

--------------------

Name:       Bjørn Kristian Punsvik
Role:       Software Developer
Position:   Senior Solution Consultant
Location:   Trondheim
Uptime:     29 years
Experience: 5 years
Education:  B.Sc. Computer Science, NTNU
```
<!-- element style="font-size: 1em;padding-bottom: 10px;" -->
</split>
note:
- Briefly introduce yourself and your experience with team dynamics at Equinor.

---

::: title

# What are Team Topologies?

:::

<grid drag="50 70" drop="left">
![[team-topologies.png|200]]
</grid>

<grid drag="50 70" drop="right">
![[team-topologies-core-ideas.jpg]]
</grid>

note:

- Define Team Topologies and its significance in modern team dynamics.
- The team is the unit of delivery
- Draw attention to the "team-first approach" as the unit of delivery.
- building fundation on refferences
- text book - the team, how to deliver value, dynamic evolving

---
::: title

#  Fundamental Team Types

:::
<grid drag="52 70" drop="left" style="padding-left: 20px;">

### Team Types

1. **Stream-aligned Team**: \
A team aligned to a single, valuable stream of work.

2) **Enabling Team**:\
Team(s) composed of specialists in a given technical (or product) domain; they help bridge the capability gap.
3) **Complicated Subsystem Team**:\
 Responsible for building and maintaining a part of the system that depends heavily on specialist knowledge.
4) **Platform Team**:\
Enables stream-aligned teams to deliver work with substantial autonomy.

### Interaction Modes

1) **Colaboration**:\
Team(s) working closely together with another team.
2) **X-as-a-Service**: \
Consuming or providing something with minimal collaboration.
3) **Facilitating**: \
Team(s) helping (or being helped by) another team to clear impediments.

</grid>

<grid drag="45 70" drop="right">
![[team-topologies-types.png]]
</grid>

note:

- Explain each team type and interaction mode with simple examples.
- Highlight how these types are designed to address specific organizational issues.
- DDD Core and supporting domain

---
::: title

# Primary interraction modes

:::
![[team-topologies-primary-interraction-modes.jpg|500]]

note:
common configuration

---
::: title

# Recursive topology

:::

![[teamtopologyrecursive.jpg|500]]

note:

---
::: title

# Mel Conway’s law

:::
> Law coined by Mel Conway that states that system design will copy the communication structures of the organization which designs it.

![[team-topologies-conways-law.png|500]]

note:

- Emphasize how organizational silos affect software design and delivery.
- Advocate for aligning team communication patterns with desired architecture.

---
::: title

# Team API

:::

<grid drag="50 70" drop="left">
![[20241208_125107.jpg]]
</grid>
<grid drag="50 70" drop="right">
![[team-topologies-team-communication.jpg]]
</grid>

note:
Share why defining clear APIs between teams is crucial (use a case study if applicable).
teams communicating through defined boundaries vs ad-hoc communication.

---

::: title

# Case Study: FOS SW/NS Team

:::

![[fos-team.png]]

note:
Roller: Ops, proj.mgmt., Dev.

A dynamic team that operates and manages 14 applications in the SafeWork and non-SAP portefolio in the Facility & Operations Solution (FOS) domain. This includes integration of database handeling, server administration, infrastructure in the cloud, and customer support. In addition the team acts as the interface between Equinor and the 3.-party ventors.

Stream-aligned

---
::: title

# Shifting Responsibilities Bring New Opportunities

:::
<split even gap="5" >

> [!info] What Changed?

> [!warning] The Challenge

</split>
note:
The team took ownership of integration, Project Management, and Development -responsibilities. integrations -> data driven

Starting from scratch in development posed difficulties.
Inconsistent project management and scattered knowledge of engineering principles.
While the team had deep domain knowledge, they faced a steep learning curve in integrating modern development workflows.

The team was exceptionally knowledgeable in their domain but lacked the development experience needed for launching integrations independently.
This gap created a unique learning opportunity.

---
::: title

# Topology

:::
<grid drag="50 70" drop="left">
**Stream Team**: FOS SW/NS\
**Enabling Team**: Bjørn Kristian\
**Platform Team**: Radix
</grid>

<grid drag="50 70" drop="right">
![[team-topology-.png]]
</grid>

note:

---
::: title

# Key Improvements

:::
<split even >
> [!info] Improve ways of working

> [!info] Knowledge Sharing and Mentoring

> [!info] Development Support
</split>
note:
My aim was very clear: to act as an enabler, not a firefighter. I came to complement the team’s strengths by supporting them in three specific areas: integration, mentoring, and development.

For example, I introduced tools and workflows that made tasks like API integration more straightforward, mentored them on reusable engineering practices.

The goal was always to empower the team to thrive independently.

---
::: title

# Transition to GitHub

:::

<split even >
![[github-1.png|450]]

![[github-2.png|450]]
</split>

note:
Lettere prosjektstyring.
Tettere kobling til utvikling.
Scope, definere, kategorisere, prioritere og estimere.
Repportere estimat.
Easy to tag team members and discuss the issue
Starting to work more as a devops team

---
::: title

# Documentation and Processes

:::

![[team-wiki.png|600]]

note:
CI -> inventory management
Team wiki -> Onboarding,

---
::: title

# Documentation and Processes

:::

![[adr.png|600]]

note:

- adr

---
::: title

# Development Support

:::

![[dev-support.png]]

note:

- Task Automation:Developed a Command-Line Interface (CLI) tool to automate test user creation, improving efficiency and reducing manual overhead.
- API Client Generation:Built a working prototype using Microsoft Kiota with OAuth2 Authentication and designed a generic method to generate API clients from Open API Specifications.
- Refactoring for Scalability:Conducted a complete refactor of the Admin CLI architecture, improving functionality by connecting with role groups and sites more effectively.
- Repository Maintenance and Integration:Maintained GitHub repositories by adding static code analysis (e.g., SNYK) and consolidating integration efforts into a mono repository to establish a single source of truth.
- Deployment Improvements:Utilized Radix (PaaS) to streamline and manage application deployments, ensuring scalability and alignment with modern cloud engineering standards.

---
::: title

# Knowledge Sharing and Mentoring

:::
<split even >
> [!info] Workshops and Pair Programming

> [!info] Guidelines and Principles

> [!info] Team Collaboration
</split>

note:
Workshops and Pair Programming:  
Conducted workshops and pair programming sessions to onboard and upskill team members on integration workflows and best practices.

Guidelines and Principles:  
Shared engineering principles such as SOLID, DRY, and YAGNI, and introduced PlantUML for effective system architecture diagramming.

Team Collaboration:  
Worked closely with team members to clarify roles, improve understanding of tools, and enhance collaboration between distributed teams.

---
::: title

# Results and Impact

:::

<grid drag="50 70" drop="left">
## What Was Achieved
1. Streamlined development environment.
2. A base platform for integrations.
3. Defined direction.
</grid>
<grid drag="50 70" drop="right">
## Team Growth
1. Gained proficiency in engineering principles, tooling, and workflows.
2. Confidence in handling integrations independently without external intervention.
3. Established reusable knowledge through documentation.
</grid>
note:
Talk about the long-term benefits of enablement: sustained development success and improved confidence amongst team members.

- Empowered team now handles integrations independently.
- Clear documentation and reusable knowledge bases.
- Better collaboration and workflow.

---
::: title

# Key Takeaways

:::

<grid drag="50 70" drop="left" style="padding-left:20px;">
### Why Continue Using This Approach?
**Empowerment Leads to Success**\
The success with the FOS AM team shows that helping teams become self-sufficient leads to better results.

### Future Opportunities

**Broaden Enabling Practices**\
By applying these enabling practices to other teams, we can boost their skills and improve overall project outcomes.
</grid>

<grid drag="50 70" drop="right">
![[team-topologies-core-ideas.jpg]]
</grid>

note:

- Summarize the key takeaways from your presentation.
- Reinforce the value of understanding and applying Team Topologies in team dynamics.
- Provide actionable advice for attendees: tips on identifying team structures and evolving them iteratively.
- handle tomorrow’s challenges independently.
- Enabling teams are a catalyst
- Uppskill not firefighting
- Enabling teams work if the organization facilitates this kind of working

---

<!-- slide template="" -->

# Q&A

![[slido-subsurface-workshop.png|500]]
