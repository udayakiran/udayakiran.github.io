---
layout: post
title: "Learnings Managing An Enterprise Scale Architecture Migration"
description: "Large scale system migrations have lots of impact on organizations, people and culture. Cost is too high some times."
tags: [Leadership, Enterprise, Scalability, Architecture, Program Management]
image:
  feature: abstract-6.jpg
  color: "616161"
  icon: "clock-o"
bg_color: "616161"
---


Architecture Migrations are not easy, especially when done for legacy systems that are tier-1, promising four 9 availability.

I consider myself lucky to be part of a large architecture revamp happened at one of my previous employers. To explain the scale of this - it was executed for 2+ years by a team of 200+ engineers fulltime. 

<div style="text-align: center">
<figure class="full">
	<img src="/images/sm.png" width="600px" alt="">
</figure>
</div>

There were 30+ micoservices almost re written and launched while dealing live traffic of 100k+ requests per sec and a huge transactional impact. As this was a platform there were atleast 2000 engineers from various client teams who were indirectly part of this as they were upstream/downstream services to this. This program had a long lasting impact on my engineering and leadership approach. Sharing some of the lessons learnt here. 

Large scale migrations leave lasting impact on your systems, people, culture and customers. They need to be avoided if possible :) Else, be executed with real thoughtgulness.

### **Lesson 1 – Ask why do you really need to re-architecture?** Focus on impact.

Be very clear about why do you want to really re-architecture your systems. Ask as many people / stakeholders as possible for the pain points and probe the engineers enough to ensure the proposed architecture redesign solves for the **right** pain points. Some of the common reasons for rearchitecture include - 

- **Stability:** Breakdown unstable/high resource consuming monoliths into smaller systems.
- **Scale and Better performance:** Improve latencies or resource usage of system to ensure it scales up right.
- **Cost savings:** Replace costly software components with cheaper ones or save resources.
- **Operational improvements:** Speed up operations, automate, reduce time, make systems self service for users.
- **Technical Debt:** Too much of a tech debt causing problems in longer term.
- Compliance / Security requirements.
- and etc.

### **Lesson 2 – Avoid if possible** !

Long running migrations almost always cause business hurdles, people issues/attrition and lack of motivation. There is huge cost involved. So, try avoiding them. Modren apps are all microservices. It's easier to really identify, isolate problems. Identify what are the reasons to re-architecture. Can this excercise be avoided with smaller tweaks to current system? Also, identify what parts of system to be modified / redesigned without having to rewrite entire system. You might be smart and lucky if you can solve for the problems without having to write a lot of code. Some tips / common scenarios where large migrations can be avoided - 

- Speed increase can be achived by adding new caching layers, run time data structures without having to change underlying write time infra.
- Identify the bottlenecks in system and only solve for them incrementally as long as they work.
- See if any process changes or support tooling can avoid these large scale migrations.

### Lesson 3 – Plan, Plan better. Review, Review again!

Like for any large projects, redesign needs to be planned well. If yours is a legacy system, involve engineers as early as possible to prepare a plan of execution. Be sure to consider side effects across the ecosystem. Do a through analysis of your legacy storage structures and data to ensure proposed new architecture fits well. Do multiple design reviews and wet your execution plan to cover missing cases. Review the plan with senior most team members.

- Assume that you will miss timelines, always almost. Plan contingencies as early as you can.
- Be prepared for unforeseen hurdles.
- Plan clear cadance for stakeholders.
- Identify the dependencies, critical path early and ensure program has focus on it always.
- Always have iterative and out come focused steps. 

### Lesson 4 – Prioritze - Think timelines, People and Business impact.

You do not need to execute all planned migration tasks to achive the most significant impact. Going by 80-20 rule, just priotize the tasks considering the maximum business impact and reuducing timelines. Some of the tasks during migrations like data movement, testing all use cases and etc, are mundane and have potential impact on people. Ensure this is taken into a/c.

- Prioritize well. Put price on each task and ask "why" you need each of them.
- Timelines will slip. Almost always. So, be prepared to have your review process that mitigates and buffers missed timelines.
- Rotate tasks as required and keep people owners to specific and challenging tasks.
- Create swim lanes where individuals or small groups can run in parallel. A long running migration program is not good for entire org's sentiment.
- Consider operational efforts and try automating them in a timely manner to avoid any business impact.

### Lesson 5 – Be Open - Consider your business, customers and their changing plans

Plans change always and it's important to stay agile and be accomodative. Your stakeholders, customers always need to be kept in touch and be checked against changing requirements and use cases to avoid blocking them on things.

- Timelines slip and can block other items of your clients they had in plan like marketing efforts, downstream system changes and etc. Keep in loop always to ensure this is mitigated.

- Scale, traffic demands and etc. always change. Be open to buffer in new system.

- For longer term migrations, it;s hard to keep the systems frozen for entire duration. Have plans to unblock your dependents.

  

  ### Lesson 6 – Have success metrics at each iteration

Once you have identifed your iterations and prioritized them, you must ensure each of the iteration has a SMART goal associated with it. Each iteration's success is important to be identified sooner than later. Besides the success metrics, have a process to integrate different component soon and measure the end to end impact early in the process.

- Have regular cadance to review the metrics upon migration. 
- Baseline performance and behavioural metrics soon at component level.

### Lesson 7 – Build Your Gaurd Rails and Tooling Well

You must focus on building required tooling and safe gaurd mechanisms for your project. Some of them include.

- Project management and collaboration tools.
- Migration scripts, testing frameworks.
- Integration and deployment tooling.
- Monitoring dashboards with system performane and task progress.
- Tools to ensure correctness of the outcomes in new system compared to older system.
- Regular review tools.
- and etc.

### Lesson 8 – Have a Dial up / Go live Strategy

<div style="text-align: center">
<figure class="full">
	<img src="/images/migrating-kubernetes-app-to-saas-managed-service-with-portworx.png" width="600px" alt="">
</figure>
</div>

Some systems are hard to validate before going live. A good amount of preparation ensures that there is a zero downtime and smooth launch for new systems. Items to keep in mind.

- Embrace some sort of shadow environments where new system runs as a shadow with live traffic but real responses would be given by earlier system. Use this live traffic to ensure correctness of new system under live traffic conditions.
- Go live early. Test it with less percentage of non critical traffic.
- Prepare tooling to be able to take smaller level entiries live. You can pick up parts of the system, data and use cases and be able to incrementally take it live.

### Lesson 9 – Have a Longer term Rollback Plan

You must always have a longer term rollback plan. Give enough of time for new system to run under production conditions but do not shutdown the earlier system in a hurry. Some of the problems surface slow and late, even a few months down the line. Have a phased cooling down period for older system and have a way to revert back to older system at some point. 
