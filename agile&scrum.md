__Agile__ → methodology for approaching software development. It consists of different frameworks such as SCRUM or Kanban that help teams continously build, test, and gather feedback on their product. It consists of four core principles:
1. Individuals and interactions over processes and tools;
2. Working software over comprehensive documentation;
3. Customer collaboration over contract negotiation;
4. Responding to change over following a plan.

## The Waterfall Method
__Waterfall__ → linear approach to building a product. A development practice previously used.
1. __Requirements__: teams spend weeks/months drafting product requirement documents. One massive document is put together outlining the product requirements in extreme detail.
2. __Design__: the architecture for the software is developed.
3. __Implementation__: everything is coded.
4. __Verification__: bug fixing.
5. __Maintenance__: the product is shipped to production, and maintenance commences.

This is a very long and laborious process in which some things get missed. There's no flexibility to implement changes, and the client is not included in the process. The waterfall methodology waits to deliver the whole product until the very end.

## How Agile Solved Waterfall Method Problems
Agile allows product development teams to continously build features that add value. The teams also are able to get feedback on their work and make changes as necessary.

Teams consistenly <mark>ship small pieces of code to production at a rapid pace</mark>. Testing also goes faster since we are only testing the compatibility of the latest piece of code.
1. A single small feature is requested.
2. The feature is coded and tested.
3. Feedback is gotten.
4. If the client is happy, it's then shipped to production.

## The Principles
#### #1: Individuals and interactions over processes and tools
Instead of forcing people to comform to strict ideation and specifications, we give them more space to experiment. Individual team members can innovate.

#### #2: Working software over comprehensive documentation
Instead of verbose specifications and planning, just write a few lines of code that work. Test it, get feedback, and shit it.

#### #3: Customer collaboration over contract negotiation
Build something small and see if your customers like it. If they do, keep going. This promotes a quick feedback loop to get the customer involved.

#### #4: Responding to change over following a plan
Using Agile teams can respond to change by listening to customer feedback and making necessary adjustments. Roadmaps always change.
> “We can’t change the direction of the wind. We can only adjust our sails.”

# Scrum
__Scrum__ → agile project management framework that teams use to develop, deliver, and sustain complex products. A product is build in a series of iterations called sprints, breaking down big complex projects into bite-sized pieces.

Scrum is structuted to help teams naturally adapt to changing conditions and user requirements, with re-prioritization built into the process and short release cycles so the teams chan constantly learn and improve.

## Scrum artifacts
__Artifacts__ → something that we make to solve a problem. In Scrum, these are:
- __Product backlog__ → master list of work that needs to get done, such as user stories, bugs, design changes, customer requests, etc. It's maintained by the Product Owner or Product Manager. Essentially, it's the team's “To Do” list. It also serves as the foundation for the iteration planinng.
- __Sprint backlog__ → list of items, user stories, or bug fixes, selected by the development team for implementation in the current sprint cycle. It may be flexible, and can evolve during a spring, but the fundamental goal cannot be compromised.
- __Increment__ (or Spring Goal) → the usuable end-product of a spring.

There are a lot of variations within artifacts that a team can choose to define.

## Scrum Ceremonies or Events
__Ceremonies__ → set of sequential events, ceremonies or meetings that scrum teams perform on a regular basics. They may change from team to team, since not all teams have the same needs.

### Organize the backlog (backlog grooming)
Responsability of the Product Owner. They maintain this list using feedback from users and the development team to help prioritize and keep the list clean and ready to be worked on at any given time.

### Sprint planning
Meeting where the work to be performed (scrope) during the current spring is planned by the entire development team. It's lead by the Scrum Master. At the end of the planning meeting, every Scrum Member must have a clear idea what needs to be done.

Ideally, spring planning should be constrained to no more than one hour for each week of sprint. The Scrum Master is responsible for making sure the meeting happens within that limit. There's not minimum time allowed.

### Sprint
The actual time period when the scrum team works together to finish an increment. Two weeks is the typical length. Dave West advises the more complex the work and the more unknowns, the shorter the sprint should be. All events - from planning to retrospective - happen during the spring. Once the length is set it should remain consistent throghout the development period.

### Daily Scrum or Stand Up
Super-short meeting that happens at the same time (usually morning) and place to keep it simple. It's goal is for everyone on the team to be on the same page. <mark>The stand up is the time to voice any concerns we ahve with meeting the sprint goal or any blockers.</mark>

Three simple questions can be used to generate a structure for the Stand Ups:
- What did I work on yesterday?
- What am I working on today?
- What issues are blocking me?

### Sprint review
At the end of the sprint, the team gets together to view a demo of, or inspect, the increment. The Product Owner can decide whether or not to release the increment. The product backlog is also reworked based on the current spring.

This is the time to ask questions, try new features, and give feedback.

### Sprint retrospective
The team comes together to document or discuss what worked and what didn't work. The idea is to create a place where the team can focus on what went well and what needs to be improved for the next time.

## Primary Roles
### Product Owner
They are focused on understanding business, customer, and market requirements, then prioritizing the work to be done accordingly.

The Product Owner is not always the Product Manager. They focus on ensuring the development team delivers the most value to the business. It's important for them to be an individual.

### Scrum Master
They coach teams, product owners, and the business on the scrum process, and look for ways to fine-tune their practice of it. They ensure the scrum framework is followed.

An effective scrum master deeply understands the work being done by the team and can help the team to optimize their transparency and delivery flow. They schedule the resources for the scrum ceremonies.

### Development Team
They are the ones who actually do the development of the product. They can be a combination of programmers, testers, designers, ops engineers, etc.

The development team is the one who drives the plan for each sprint. They forecast how much work they believe they can complete over the interation.

# Sources
[Agile Methods and Methodology for Beginners – FreeCodeCamp](https://www.freecodecamp.org/news/agile-methods-and-methodology-for-beginners/)\
[Atlassian Agile Coach](https://www.atlassian.com/agile/scrum)