---
title: "The Principles of Product Development Flow — Donald G. Reinertsen (2009)"
tags: [sources, reinertsen, flow, product-development, queues, wip, cost-of-delay, lean]
---

# Principles of Product Development Flow — Source Notes

**Book:** The Principles of Product Development Flow: Second Generation Lean Product Development
**Author:** Donald G. Reinertsen (2009)

**Sources fetched:** 2026-04-16

- https://blackswanfarming.com/cost-of-delay/
- https://blackswanfarming.com/cost-of-delay-divided-by-duration/
- https://en.wikipedia.org/wiki/Cost_of_delay
- https://en.wikipedia.org/wiki/Little%27s_law
- https://en.wikipedia.org/wiki/Kanban_(development)
- https://martinfowler.com/articles/products-over-projects.html
- https://www.goodreads.com/book/show/6278270 (book description + reviews)

---

## Source: https://blackswanfarming.com/cost-of-delay/

Cost of Delay | Black Swan Farming

-->

BLACK

SWAN

FARMING

640px wide screens only -->

Search

-->

BLACK

SWAN

FARMING

640px wide screens only -->

Search

-->

Cost of Delay

"Cost of Delay is the golden key that unlocks many doors. It has an astonishing power to transform the mindset of a development organisation." – Donald G. Reinertsen

Cost of Delay is a way of communicating the impact of  time  on the  outcomes  we hope to achieve. More formally, it is the partial derivative of the total expected value with respect to time.

Cost of Delay  combines

urgency

and

value

– two things that humans are not very good at distinguishing between. To make decisions, we need to understand not just how valuable something is, but how urgent it is.

Why is it the “One Thing” to Quantify?

The value that we miss out on when we deliver slowly or “late” can be enormous. It is often far more valuable to get something even a week earlier than it is to make it slightly cheaper to develop. These trade-offs are not obvious though – unless we understand the Cost of Delay.

Improve prioritisation

Use Cost of Delay to surface assumptions & focus on what's valuable and urgent. CD3 (Cost of Delay Divided by Duration) helps you get more of what you want, faster.

If you want to move on from prioritisation by gut-feel, MoSCoW hell or HiPPO-driven decisions, you need to understand  Cost of Delay.  More

Make better tradeoff decisions

Product Development is full of tradeoffs. Use Cost of Delay to better inform these decisions and get distributed decision-making at all levels in your organisation.

What are our queues costing us? What is the value of doing more frequent releases? What should our WIP limits be? Does it make sense to increase our capacity?  More

Change the conversation

If the system has little information available about value and urgency, it will optimise for other things – typically cost and dates, which drive the wrong behaviours

Read the Case Study of applying Cost of Delay across the portfolio at Maersk Line – and the way conversations started to be oriented around value and urgency.  More

Interested, but not sure how to get started? We’ve done this for lots of different organisations: from Fortune 500 giants like Maersk Line to smaller startups — as well as public and private sector organisations.

To get you started, we’ve written a short

four step guide to quantifying Cost of Delay  to help you learn the ropes and start applying Cost of Delay in your organisation. If you’re struggling with quantifying value or understanding urgency, you could also start with  a simple and easy-to-use qualitative approach , to help you learn the ropes.

A case study – Maersk Line

The value of quantifying Cost of Delay really becomes clear when you see it in action. For example, below is a value stream map for a feature that was delivered by a team at Maersk Line:

38 weeks of waiting seems crazy, doesn’t it? The things is, if you were to track the time spent adding value versus the time spent waiting in your organisation you will probably find something similar. In most organisations the end-to-end cycletime is dominated by waiting time.

The incredible cost of queues

In the example above, the Cost of Delay for this feature was actually more than  $200,000 per week!

So, the 38 weeks that this opportunity spent waiting in various queues cost the organisation nearly $8m in lost revenue.

Knowing this puts the cost of waiting into perspective, doesn’t it? If they had taken the 5 minutes needed to estimate the Cost of Delay for this feature then a number of key decisions would have been made quite differently.

It’s one thing for an organisation to be blind to queues. It’s another level of blindness to have no clue what those queues are costing. If we’re going to make better decisions, we really need to understand the Cost of Delay of the things flowing through the system.

Optimising for speed

Like most organisations, Maersk was focused more on the efficiency of the  parts of the process, than the speed of the end-to-end delivery of value.

For instance, it is normal to find  approval and funding processes  that are optimized for the efficiency of those doing the approving, seriously impacting the speed and efficiency of the whole system. Maersk Line, of course, was the same.

Part of what drives these poor system-design decisions is that we have a really bad understanding of how much the delays are actually costing us. 


---

## Source: https://blackswanfarming.com/cost-of-delay-divided-by-duration/

Cost of Delay Divided by Duration | Black Swan Farming

-->

BLACK

SWAN

FARMING

640px wide screens only -->

Search

-->

BLACK

SWAN

FARMING

640px wide screens only -->

Search

-->

Cost of Delay Divided by Duration

CD3: C

ost of

D

elay

D

ivided by

D

uration

is a prioritisation/scheduling method that maximises the value delivered in a given time period when you have limited capacity.

It is particularly useful in environments where a primary constraint of the system is the available time of a relatively fixed or "scarce" resource. This matches product development very well, because of the communication, collaboration and coordination overheads, which constrain our ability to increase capacity.

CD3 is one specific form of the "WSJF – Weighted Shortest Job First" queuing method.

We could choose weight by other things (risk, stakeholder importance, length of time waiting, etc). In the case of CD3 we are weighting by

Cost of Delay  . (Saying "Cost of Delay Divided by Duration" more than a few times get rather tiring, so to ease communication we can shorten this to CD3.)

One of the benefits of CD3 is that it enables us to use a common measure to compare opportunities with different value and urgency, and where the duration differs. CD3 optimises the Return on Investment by minimising the total  Delay Cost  incurred, given a set of potential options. In most product development settings, capacity is relatively inflexible and constraints on scaling beyond certain limits. Because of this, even a very rough understanding how long the pipeline is likely to be blocked for is quite valuable information – it can change the order in which we decide to schedule work. Because CD3 uses Duration on the denominator, it also has the benefit of encouraging the breakdown of work into smaller batches. Breaking down work and delivering in smaller batch sizes is one of the easiest, cheapest and most effective improvements we can make in terms of getting more value, faster flow and better quality.

When using CD3, the priority order of features (or initiatives/projects) is determined by dividing the estimated Cost of Delay by some estimate of duration: the higher the resulting score, the higher the priority.

Comparing CD3 to other prioritisation methods:

Let’s use an example to demonstrate how and why CD3 improves Return on Investment. Consider the following three features:

Cost of Delay

Duration

CD3 Score

Feature A

$1,000/week

5 weeks

200

Feature B

$4,000/week

1 week

4,000

Feature C

$5,000/week

2 weeks

2,500

Using these three features we can look at the impact to two alternatives to how we might schedule them. We could choose to work on and deliver these features one at a time in the order they arrived. A, then B, then C. (This is called First In, First Out. It is a common scheduling approach in manufacturing). After all, the person asking for Feature A will have been waiting for the longest time so we really should serve them first. Then B, and then C.

For the 5 weeks we are working on Feature A we incur the Cost of Delay of all three features: $5,000/wk + $4,000/wk + $1,000/wk. This adds up to $10,000/week times 5 weeks giving us a total Delay Cost incurred so far of $50,000.

We then move on to developing Feature B. For the 1 week this takes us to deliver we incur the Cost of Delay of Features B and C: $4,000/week + $5,000/week = $9,000/week. So the Delay Cost is an additonal $9,000, bringing us to a total of $59 worth of Delay Cost incurred so far.

At last, we can start working on Feature C. incuring the Cost of Delay of C during it's development of $5,000/week for the two weeks it takes to build Feature C. This is another $10,000 of Delay Cost to add to our previous of $59,000 for a total of $69,000 Delay Cost incurred.

Or, use CD3: Cost of Delay Divided by Duration

Let's consider another way of processing these Features. If we work on the features based on whichever has the highest CD3 score we would do Feature B first, followed by Feature C, and finally Feature A.

For the 1 week we are working on Feature B we incur Cost of Delay of $(4k+5k+1k)/week. Delay Cost = $10,000 For the 2 weeks we are working on Feature C we incur Cost of Delay of $(5k+1k)/week. Delay Cost = $12,000 For the 5 weeks we are working on Feature A we incur Cost of Delay of $1k/week. Delay Cost = $5,000

Total Delay Cost using CD3 is $27,000 a 61%  decrease  in the Delay Cost.

As you can see, using CD3 to order your backlo


---

## Source: https://en.wikipedia.org/wiki/Cost_of_delay

Cost of delay - Wikipedia

Jump to content

Main menu

Main menu

move to sidebar

hide

Navigation

Main page

Contents

Current events

Random article

About Wikipedia

Contact us

Contribute

Help

Learn to edit

Community portal

Recent changes

Upload file

Special pages

Search

Search

Appearance

Donate

Create account

Log in

Personal tools

Donate

Create account

Log in

Contents

move to sidebar

hide

(Top)

1

Cost of Delay in Product Development

2

Cost of Delay in Finance

Toggle Cost of Delay in Finance subsection

2.1

A simple delayed investment example

3

See also

4

References

Toggle the table of contents

Cost of delay

1 language

Türkçe

Edit links

Article

Talk

English

Read

Edit

View history

Tools

Tools

move to sidebar

hide

Actions

Read

Edit

View history

General

What links here

Related changes

Upload file

Permanent link

Page information

Cite this page

Get shortened URL

Print/export

Download as PDF

Printable version

In other projects

Wikidata item

Appearance

move to sidebar

hide

From Wikipedia, the free encyclopedia

Financial measurement

Cost of Delay  is "a way of communicating the impact of time on the outcomes we hope to achieve".

1

More formally, it is the  partial derivative  of the  total expected value  with respect to  time . Cost of Delay combines an understanding of value with how that value leaks away over time.  It is a tactic that helps communicate and prioritize development decisions by calculating the impact of time on value creation & capture.

2

More simply, it is the answer to the question: "What would it cost us if this was delayed by 1 month?". Or, alternatively, "what would it be worth to us if we could get this 1 month earlier?"

Cost of Delay has the units of $/time. The Delay Cost incurred (as a result of a delay) is found by integrating Cost of Delay over a specific time period.

Cost of Delay in Product Development

[

edit

]

Cost of Delay is described by Don Reinertsen as being the "one thing" to quantify. "We need Cost of Delay to evaluate the cost of queues, the value of excess capacity, the benefit of smaller batch sizes and the value of variability reduction. Cost of Delay is the golden key that unlocks many doors. It has an astonishing power to totally transform the mind-set of a development organisation."

2

Reinertsen reports that ~85% of product managers do not know the Cost of Delay.

3

He also reports that intuition of Cost of Delay is poor, with the spread of intuitive estimates differing by 50 to 1.

4

For this reason it is worth making the effort to  quantify  the Cost of Delay.

Cost of Delay is also useful for making better decisions wherever there is an opportunity to sacrifice time for other key variables of the product. Another common usage is as the weighting in a Weighted Shortest Job First (WSJF) scheduling algorithm, for improved prioritisation. This is sometimes referred to as "CD3" – Cost of Delay Divided by Duration. The CD3 algorithm works by maximising the total value delivered in any given time period by a scarce development capacity.

Cost of Delay in Finance

[

edit

]

From a financial investment perspective, a delay in making an investment can lead to a loss. The  accrued interest  on the investment for the duration of the delay can have a significant effect on the net returns. The cost grows with the period of the investment; the longer the investment is delayed, the higher the cost is.

A simple delayed investment example

[

edit

]

Reduced value of the Maturity Amount with various delays

Alberto is planning to invest $6,000 at an expected interest rate of 10%, compounded annually. He needs the money 5 years from now.

If there is a delay in making this investment, Alberto incurs a Delay Cost, depending on how long the investment is delayed, as shown in the chart – up to $600 for an 8-month delay.

Investment

Amount

Period

Interest rate

Compounding

Delay period

6000.00 USD

5 Year

10.00%

Annually

8 Month

Returns

Interest Accrued

Maturity Amount

US$3,068.17

US$9,068.17

See also

[

edit

]

Finance

Interest

Real interest rate

Single deposit

Periodic deposit

References

[

edit

]

^

"Using Cost of Delay to Quantify Value and Urgency"  . Retrieved  21 June  2016 .

^

a

b

Reinertsen, Donald  (2009).  The Principles of Product Development Flow . Celeritas.  ISBN

978-1-935401-00-1  .

^

"Getting flow into your product development" . 11 April 2011 . Retrieved  21 Ju


---

## Source: https://en.wikipedia.org/wiki/Kanban_(development)

Kanban (development) - Wikipedia

Jump to content

Main menu

Main menu

move to sidebar

hide

Navigation

Main page

Contents

Current events

Random article

About Wikipedia

Contact us

Contribute

Help

Learn to edit

Community portal

Recent changes

Upload file

Special pages

Search

Search

Appearance

Donate

Create account

Log in

Personal tools

Donate

Create account

Log in

Contents

move to sidebar

hide

(Top)

1

Kanban boards

2

Kanban practices

3

Managing workflow

4

Evolution and documentation of method

5

See also

6

References

7

Further reading

Toggle the table of contents

Kanban (development)

17 languages

العربية

Български

Català

Deutsch

Español

فارسی

Français

Magyar

Հայերեն

日本語

한국어

Polski

Русский

Türkçe

Українська

粵語

中文

Edit links

Article

Talk

English

Read

Edit

View history

Tools

Tools

move to sidebar

hide

Actions

Read

Edit

View history

General

What links here

Related changes

Upload file

Permanent link

Page information

Cite this page

Get shortened URL

Print/export

Download as PDF

Printable version

In other projects

Wikimedia Commons

Wikidata item

Appearance

move to sidebar

hide

From Wikipedia, the free encyclopedia

A major contributor to this article appears to have a  close connection  with its subject.

It may require cleanup to comply with Wikipedia's content policies, particularly  neutral point of view . Please discuss further on the  talk page .  See our  advice if the article is about you  and read our  scam warning  in case someone asks for money to edit this article.

( August 2022 )

(  Learn how and when to remove this message  )

Workflow management method

This article is about the process-management and improvement method. For the lean-manufacturing process, see  Kanban .

A  Kanban board

Part of a series on

Software development

Core activities

Data modeling

Processes

Requirements

Design

Construction

Engineering

Testing

Debugging

Deployment

Maintenance

Paradigms and models

Agile

Cleanroom

Incremental

Prototyping

Spiral

V model

Waterfall

Methodologies  and frameworks

ASD

DAD

DevOps

DSDM

FDD

IID

Kanban

Lean SD

LeSS

MDD

MSF

PSP

RAD

RUP

SAFe

Scrum

SEMAT

TDD

TSP

UP

XP

Supporting disciplines

Configuration management

Deployment management

Documentation

Project management

Quality assurance

User experience

Practices

ATDD

BDD

CCO

CD

CI

DDD

PP

SBE

Stand-up

TDD

Tools

Build automation

Compiler

Debugger

GUI builder

IDE

Infrastructure as code

Profiler

Release automation

UML Modeling

Standards and bodies of knowledge

CMMI

IEEE standards

IREB

ISO 9001

ISO/IEC standards

ITIL

OMG

PMBOK

SWEBOK

Glossaries

Artificial intelligence

Computer science

Electrical and electronics engineering

Outlines

Software development

C programming language

C sharp programming language

C++ programming language

Java programming language

JavaScript programming language

Python programming language

Rust programming language

v

t

e

Kanban  ( Japanese :

看板

, meaning

signboard

or

billboard  ) is a

lean method  to manage and improve work across human  systems . This approach aims to manage work by balancing demands with available capacity, and by improving the handling of system-level  bottlenecks .

Work items are visualized to give participants a view of progress and process, from start to finish—usually via a  kanban board . Work is  pulled  as capacity permits, rather than work being pushed into the process when requested.

In

knowledge work  and in  software development , the aim is to provide a visual  process management  system which aids decision-making about what, when, and how much to produce. The underlying  kanban  method originated in  lean manufacturing ,

1

which was inspired by the  Toyota Production System .

2

It has its origin in the late 1940s when the Toyota automotive company implemented a production system called just-in-time, which had the objective of producing according to customer demand and identifying possible material shortages within the production line. But it was a team at Corbis that realized how this method devised by Toyota could become a process applicable to any type of organizational process. Kanban is commonly used in software development in combination with methods and frameworks such as  Scrum .

3

Kanban boards

[

edit

]

Main article:  Kanban board

The diagram here shows a software development workflow on a kanban b


---

## Source: https://en.wikipedia.org/wiki/Work_in_process

Work in process - Wikipedia

Jump to content

Main menu

Main menu

move to sidebar

hide

Navigation

Main page

Contents

Current events

Random article

About Wikipedia

Contact us

Contribute

Help

Learn to edit

Community portal

Recent changes

Upload file

Special pages

Search

Search

Appearance

Donate

Create account

Log in

Personal tools

Donate

Create account

Log in

Contents

move to sidebar

hide

(Top)

1

WIP inventory in supply chain management

2

WIP inventory in accounting

3

Tax treatment

4

References

Toggle the table of contents

Work in process

13 languages

العربية

বাংলা

Deutsch

Euskara

فارسی

Français

Italiano

日本語

Nederlands

Polski

Português

Türkçe

中文

Edit links

Article

Talk

English

Read

Edit

View history

Tools

Tools

move to sidebar

hide

Actions

Read

Edit

View history

General

What links here

Related changes

Upload file

Permanent link

Page information

Cite this page

Get shortened URL

Print/export

Download as PDF

Printable version

In other projects

Wikimedia Commons

Wikidata item

Appearance

move to sidebar

hide

From Wikipedia, the free encyclopedia

Partially finished goods waiting for completion and eventual sale or value of these items

"Work in progress" redirects here. For other uses, see  Work in progress (disambiguation) .

Work in process  or  work-in-process ,  WIP ,

1

2

3

4

work in progress ,

5

6

7

goods in process ,

1

or  in-process inventory  refers to a company's partially  finished goods  waiting for completion and eventual sale, or the value of these items.

8

The term is used in  supply chain management , and WIP is a key input for calculating inventory on a company's  balance sheet . In  lean thinking , inappropriate processing or excessive processing of goods or work in process, "doing more than is necessary", is seen as one of the seven wastes (Japanese term:

muda  ) which do not add value to a product.

9

10

WIP inventory in supply chain management

[

edit

]

WIP inventory calculations can help a company assess their supply chain health and guide in supply chain planning.

11

In most cases, it is ideal to have low WIP inventory levels,

11

and companies that manage their inventory level efficiently tend to have lower costs.

12

Managing WIP inventory requires coordination between several functions within a company, as well as with suppliers and customers.

12

Higher WIP inventory levels are advantageous in that they can support a surge in demand, as well as improve cycle time since there is more material in production. However, this can also increase storage costs and obsolescence risk, as well as lead to waste if demand is lower than expected.

13

To mitigate these risks, companies are increasingly turning to demand forecasting software. These tools analyze historical data, market trends, and customer behavior to predict future demand with greater accuracy. This allows companies to optimize WIP levels, ensuring they have enough material to meet anticipated demand without carrying excessive inventory that could become obsolete.

14

WIP inventory in accounting

[

edit

]

WIP inventory refers to goods that are in production and not yet a finished good.

6

On the balance sheet, WIP inventory is aggregated into the inventory line under current assets along with raw materials and finished goods.

15

To calculate WIP inventory at the end of an  accounting period , the following 3 figures are required: beginning WIP inventory, production costs, and finished goods. Beginning WIP inventory is the WIP inventory figure from the previous accounting period. Production costs includes all costs associated with manufacturing a product, such as raw materials, labor, and overhead costs. Finished goods is the total value of goods ready for sale in the current accounting period. The formula for calculating WIP inventory is as follows: beginning WIP inventory + production costs – finished goods.

11

Tax treatment

[

edit

]

In the United Kingdom,  HMRC  has no specific definition of work-in-process, but three different types of uncompleted items are identified for tax purposes:

manufactured products

contracts for services

construction contracts

16

References

[

edit

]

^

a

b

"Work-in-process dictionary definition  work-in-process defined" . business.yourdictionary.com. Archived from  the original  on 2013-04-14 . Retrieved  2014-07-12  .

^

"WORK IN PROCESS DEFINITION" . ventureline.com . Retrieved  20


---

## Source: https://en.wikipedia.org/wiki/Little%27s_law

Little's law - Wikipedia

Jump to content

Main menu

Main menu

move to sidebar

hide

Navigation

Main page

Contents

Current events

Random article

About Wikipedia

Contact us

Contribute

Help

Learn to edit

Community portal

Recent changes

Upload file

Special pages

Search

Search

Appearance

Donate

Create account

Log in

Personal tools

Donate

Create account

Log in

Contents

move to sidebar

hide

(Top)

1

History

2

Examples

Toggle Examples subsection

2.1

Finding response time

2.2

Customers in the store

3

Estimating parameters

4

Applications

5

Distributional form

6

See also

7

References

8

External links

Toggle the table of contents

Little's law

15 languages

العربية

Català

Cymraeg

Deutsch

فارسی

Français

עברית

Italiano

日本語

Nederlands

Polski

Русский

Svenska

Українська

中文

Edit links

Article

Talk

English

Read

Edit

View history

Tools

Tools

move to sidebar

hide

Actions

Read

Edit

View history

General

What links here

Related changes

Upload file

Permanent link

Page information

Cite this page

Get shortened URL

Print/export

Download as PDF

Printable version

In other projects

Wikidata item

Appearance

move to sidebar

hide

From Wikipedia, the free encyclopedia

Theorem in queueing theory

In mathematical  queueing theory ,  Little's law  (also  result ,  theorem ,  lemma , or  formula

1

2

) is a theorem by  John Little  which states that the long-term average number of customers ( L ) in a  stationary  system is equal to the long-term average effective arrival rate (  ) multiplied by the average time that a customer spends in the system ( W ). Expressed algebraically the law is

L

=

&#x03BB;

W

.

{\displaystyle L=\lambda W.}

The relationship is not influenced by the arrival process distribution, the service distribution, the service order, or practically anything else. In most queuing systems, service time is the  bottleneck  that creates the queue.

3

The result applies to any system, and particularly, it applies to systems within systems.

4

For example in a bank branch, the  customer line  might be one subsystem, and each of the  tellers  another subsystem, and Little's result could be applied to each one, as well as the whole thing. The only requirement is that the system be  ergodic .

5

In some cases it is possible not only to mathematically relate  the  average  number in the system to the  average  wait but even to relate the entire

probability distribution

(and moments) of the number in the system to the wait.

6

History

[

edit

]

In a 1954 paper, Little's law was assumed true and used without proof.

7

8

The form  L = λW  was first published by  Philip M. Morse  where he challenged readers to find a situation where the relationship did not hold.

7

9

Little published  in 1961 his proof of the law, showing that no such situation existed.

10

Little's proof was followed by a simpler version by Jewell

11

and another by Eilon.

12

Shaler Stidham published a different and more intuitive proof in 1972.

13

14

Examples

[

edit

]

This section  needs additional citations for  verification  .  Please help  improve this article  by  adding citations to reliable sources in this section. Unsourced material may be challenged and removed.

Find sources:  "Little's law" – news  ·

newspapers  ·

books  ·

scholar  ·

JSTOR

( December 2025 )

(  Learn how and when to remove this message  )

Finding response time

[

edit

]

Imagine an application that had no easy way to measure  response time . If the mean number in the system and the throughput are known, the average response time can be found using Little’s Law:

mean response time = mean number in system / mean throughput

For example: A queue depth meter shows an average of nine jobs waiting to be serviced. Add one for the job being serviced, so there is an average of ten jobs in the system. Another meter shows a mean throughput of 50 per second. The mean response time is calculated as 0.2 seconds = 10 / 50 per second.

Customers in the store

[

edit

]

Imagine a small store with a single counter and an area for browsing, where only one person can be at the counter at a time, and no one leaves without buying something.  So the system is:

entrance → browsing → counter → exit

If the rate at which people enter the store (called the arrival rate) is the rate at which they exit (called the exit rate), the system is stable.  By contrast, an arrival rate exceeding an exi


---

## Source: https://martinfowler.com/articles/products-over-projects.html

Products Over Projects

Refactoring

Agile

Architecture

About

Thoughtworks

Topics

Architecture

Refactoring

Agile

Delivery

Microservices

Data

Testing

DSL

about me

About

Books

FAQ

content

Videos

Content Index

Fragments

Board Games

Photography

Thoughtworks

Home

Insights

Careers

Radar

Engineering

follow

RSS

Mastodon

LinkedIn

Bluesky

X

BGG

Table of Contents

Top

What is Product-Mode?

Benefits of Operating in Product-Mode

Ability to Reorient Quickly

Reduced End-to-End Cycle Time

Ability to Truly Iterate

Example: A retirement calculator

Knowledge Retention

Architectural Integrity

Ownership of Code and Systems

Team Motivation and Dynamics

Economies of Flow and Iteration

Challenges of Operating in Product-Mode

Staff Utilization

Insularity

New silos

Other Considerations

Tiered Teams

Squads and Tribes

But where is the Product?

Conclusion

Sidebars

Don&#x2019;t run it like a city

Products Over Projects

Software projects are a popular way of funding and organizing software

development. They organize work into temporary, build-only teams and are funded with specific

benefits projected in a business case. Product-mode instead uses durable, ideate-build-run teams working

on a persistent business issue. Product-mode allows teams to reorient quickly, reduces their end-to-end

cycle time, and allows validation of actual benefits by using short-cycle iterations while maintaining

the architectural integrity of their software to preserve their long-term effectiveness.

20 February 2018

Sriram Narayan

Sriram is a Digital&#x200B;-&#x200B;IT Management Consultant at Thoughtworks. He helps clients

improve the performance of their Digital/Product/Eng&#x200B;g./IT departments through

changes to&#x200B; &#x200B;their ways of working (tech operating model). His book on this topic&#x2014;

Agile IT Org Design, was

featured  &#x200B;&#x200B;as a must-read for CIOs &#x200B;by Enterprisers Project&#x200B;&#x200B;, a joint

initiative of Harvard Business Review, CIO Magazine and RedHat&#x200B;.

enterprise architecture

team organization

Contents

What is Product-Mode?

Benefits of Operating in Product-Mode

Ability to Reorient Quickly

Reduced End-to-End Cycle Time

Ability to Truly Iterate

Example: A retirement calculator

Knowledge Retention

Architectural Integrity

Ownership of Code and Systems

Team Motivation and Dynamics

Economies of Flow and Iteration

Challenges of Operating in Product-Mode

Staff Utilization

Insularity

New silos

Other Considerations

Tiered Teams

Squads and Tribes

But where is the Product?

Conclusion

Sidebars

Don&#x2019;t run it like a city

FAQ

Software projects are a popular way of funding and organizing software development.

Projects are funded on a case-by-case basis on the basis of benefits projected in a

business case. They are organized in the form of one or more temporary teams whose

members have durable reporting lines outside the project organization. They are

staffed from a &#x201C;pool of talent&#x201D; whose members are considered fungible within lines of

specialization. And usually, a software project team&#x2019;s job is to build or enhance some

system or application and move on.

However, projects are not the only way of funding and organizing software

development. For instance, many companies that sell software as a product or a service

do not fund or organize their core product/platform development in the form of

projects. Instead, they run product development and support using near-permanent teams

for as long as the product is sold in the market. The budget may vary year on year but

it is generally sufficient to fund a durable, core development organization

continuously for the life of the product. Teams are funded to work on a particular

business problem or offering over a period of time; with the nature work being defined

by a business problem to address rather than a set of functions to deliver. We call

this way of working as &#x201C;product-mode&#x201D; and assert that it is not necessary to be

building a software product in order to fund and organize software development like

this.

What is Product-Mode?

&#x201C;Product-mode&#x201D; is a way of working. It is a way of funding and organizing

software development that differs significantly from the projects way of doing it.

Although generally applicable to digital-age enterprise IT, this way of working

is especially suited to those who aim to drive busi


---

## Source: https://www.goodreads.com/book/show/6278270-the-principles-of-product-development-flow

The Principles of Product Development Flow: Second Generation Lean Product Development by Donald G. Reinertsen | Goodreads

Home

My Books

Browse ▾

Recommendations

Choice Awards

Genres

Giveaways

New Releases

Lists

Explore

News & Interviews

Loading...

Community ▾

Groups

Quotes

Ask the Author

People

Sign in

Join

Jump to ratings and reviews

Want to Read

Rate this book

The Principles of Product Development Flow: Second Generation Lean Product Development

Donald G. Reinertsen

4.19

2,529

ratings  138

reviews

Want to Read

Rate this book

"...the dominant paradigm for managing product development is wrong. Not just a little wrong, but wrong to its very core." So begins Reinertsen in his meticulous examination of today's product development practices. He carefully explains why invisible and unmanaged queues are the underlying root cause of poor product development performance. He shows why these queues form and how they undermine the speed, quality, and efficiency in product development. Then, he provides a roadmap for changing this. The book provides a well-organized set of 175 underlying principles in eight major areas. He shows you practical methods Improve economic decisions Manage queues Reduce batch size Apply WIP constraints Accelerate feedback Manage flows in the presence of variability Decentralize control The Principles of Product Development Flow will forever change the way you think about product development.

Genres

Business

Management

Nonfiction

Leadership

Technology

Software

Startup

...more

294 pages, Hardcover  First published May 1, 2009

Book details & editions

Loading...

Loading...

About the author

Donald G. Reinertsen

5

books 56

followers

Follow

Follow

Ratings  &  Reviews

What do  you  think?

Rate this book

Write a Review

Friends  &  Following

Create a free account

to discover what your friends think of this book!

Community Reviews

4.19

2,529

ratings  138

reviews

5 stars

1,256 (49%)

4 stars

726 (28%)

3 stars

376 (14%)

2 stars

104 (4%)

1 star

67 (2%)

Search review text

Filters

Displaying 1 - 30 of 138 reviews

Rod Hilton

152 reviews

3,116 followers

Follow

Follow

March 31, 2010

Don Reinertsen's book is somewhat difficult to review. There are two aspects to a book: the information it contains, and the way in which it is presented, and since my take on these two aspects of so different, I wish to speak about them separately.  In terms of the information contained in the book, it is phenomenal. Reinertsen basically takes the principles of Lean Manufacturing and explains the ways in which they can apply to product development and the ways in which they cannot. For the principles that cannot, the philosophy behind those principles is used to develop new principles for product development. These overall principles are career-changing. There's a good change your product development team is doing things wrong, and this book will show you why and what you should do instead. Information: 5/5.  The manner in which it is presented is another story. The book is dense, dry, and difficult to read. Reinertsen often assumes a level of familiarity with manufacturing terminology, economics, and management theory that readers may simply lack. He warns in his introduction that his book is very technical, but it's worse than that: the book left me in the dark a number of times, unwilling to explain terms that I think only managers or mechanical engineers could understand. It's one thing to use a STYLE that is difficult for non-engineers, but its another thing to use terminology, so I found myself often having to look up information that should have been in the book itself.  The book also comes off as very hand-wavey. Lots of graphs and figures are presented, but the sources of these graphs and figures are never made clear. Sometimes it felt like the book was simply trying to distract me from asking questions with a pretty picture.  The book is strongest when it uses examples and tries to appeal to intuition. When Reinertsen can explain why something just "makes sense", the principle sticks. When it makes no intuitive sense and Reinertsen attempts to "prove" it with graphs, the lack of hard data makes the claims seem dubious. Book: 2/5.  But while the book is difficult to get through and leaves much to be desired in terms of its writing, the information it contains is invaluable. I consider this a must-read for product development companies in the 21st ce


---
