---
title: "Part 3: You are a Senior Engineer, Communication and other Soft Skills"
date: 2022-02-15T17:57:48-03:00
description: "This is a short description"
image: /media/author.png
draft: true
---

Be Pragmatic, Yet Visionary

Visionary
Thinking about or planning the future with imagination or wisdom.

Pragmatic
Dealing with things sensibly and realistically in a way that is based on practical rather than theoretical considerations.


Find on that book the things about communication that they talk about, the software architecture one.

IRRATIONAL ARTIFACT ATTACHMENT
…is the proportional relationship between a person’s irrational attachment to some artifact and how long it took to produce. If an architect creates a beautiful diagram using some tool like Visio that takes two hours, they have an irrational attachment to that artifact that’s roughly proportional to the amount of time invested, which also means they will be more attached to a four-hour diagram than a two-hour one.

Key pillar of good communication:

1. You need to be able to explain your idea to any audience and adapt yourself to the audience.
2. You need to be fine with explaniing stuff over and over again
3. You need to be fine with questions, and even if you don't know the answer, you need to be able to say that you don't know, but you will find out.
4. Be comfortable with not knowing everything, and be open to learning from others.
5. Be comfortable with suggestions, acknowledge them respectfully, and be open to discussing them. Even if they are dumb, they might lead to a better idea.
6. Be open to feedback, and be able to give feedback in a respectful way.
7. Mentor others, the best way to learn is teaching.
8. Understand hierarchy and learn how to communicate with people in different levels of the organization. -- This is tricky for me, I don't know how to do that.
9. Get really freaking good with diagrams
10. Getting good with presentations don't hurt either
11. Push yourself out of your comfort zone
12. Learn to how speak "business"
    1.  Things like risk matrix
    2. Leverage the use of grammar and buzzwords to better understand the situation.
13. Keeping asking why and why and why
14. Negotiation, the senior engineer is about negotiating with the stakeholders for pushing the technical agenda, cleaning the tech debt, making refactors etc, while the stakeholder agenda is creating business value, these are not mutually exclusive (at least not always), learn ho to find the project that will tackle both!
15. Negotiating with other senior engineers is also very complicated


An effective way of avoiding accidental complexity is what we call the 4 C’s of architecture: communication, collaboration, clarity, and conciseness. These factors (illustrated in Figure 23-2) all work together to create an effective communicator and collaborator on the team.

## Diagraming

Diagramming Standards: UML, C4, and ArchiMate
Several formal standards exist for technical diagrams in software.

UML
Unified Modeling Language (UML) was a standard that unified three competing design philosophies that coexisted in the 1980s. It was supposed to be the best of all worlds but, like many things designed by committee, failed to create much impact outside organizations that mandated its use.

Architects and developers still use UML class and sequence diagrams to communicate structure and workflow, but most of the other UML diagram types have fallen into disuse.

C4
C4 is a diagramming technique developed by Simon Brown to address deficiencies in UML and modernize its approach. The four C’s in C4 are as follows:

Context
Represents the entire context of the system, including the roles of users and external dependencies.

Container
The physical (and often logical) deployment boundaries and containers within the architecture. This view forms a good meeting point for operations and architects.

Component
The component view of the system; this most neatly aligns with an architect’s view of the system.

Class
C4 uses the same style of class diagrams from UML, which are effective, so there is no need to replace them.

If a company seeks to standardize on a diagramming technique, C4 offers a good alternative. However, like all technical diagramming tools, it suffers from an inability to express every kind of design an architecture might undertake. C4 is best suited for monolithic architectures where the container and component relationships may differ, and it’s less suited to distributed architectures, such as microservices.

ArchiMate
ArchiMate (an amalgam of Arch*itecture-Ani*mate) is an open source enterprise architecture modeling language to support the description, analysis, and visualization of architecture within and across business domains. ArchiMate is a technical standard from The Open Group, and it offers a lighter-weight modeling language for enterprise ecosystems. The goal of ArchiMate is to be “as small as possible,” not to cover every edge case scenario. As such, it has become a popular choice among many architects.

Diagram Guidelines
Regardless of whether an architect uses their own modeling language or one of the formal ones, they should build their own style when creating diagrams and should feel free to borrow from representations they think are particularly effective. Here are some general guidelines to use when creating technical diagrams.

Titles
Make sure all the elements of the diagram have titles or are well known to the audience. Use rotation and other effects to make titles “sticky” to the thing they associate with and to make efficient use of space.

Lines
Lines should be thick enough to see well. If lines indicate information flow, then use arrows to indicate directional or two-way traffic. Different types of arrowheads might suggest different semantics, but architects should be consistent.

Generally, one of the few standards that exists in architecture diagrams is that solid lines tend to indicate synchronous communication and dotted lines indicate asynchronous communication.

Shapes
While the formal modeling languages described all have standard shapes, no pervasive standard shapes exist across the software development world. Thus, each architect tends to make their own standard set of shapes, sometimes spreading those across an organization to create a standard language.

We tend to use three-dimensional boxes to indicate deployable artifacts and rectangles to indicate containership, but we don’t have any particular key beyond that.

Labels
Architects should label each item in a diagram, especially if there is any chance of ambiguity for the readers.

Color
Architects often don’t use color enough—for many years, books were out of necessity printed in black and white, so architects and developers became accustomed to monochrome drawings. While we still favor monochrome, we use color when it helps distinguish one artifact from another. For example, when discussing microservices communication strategies in “Communication”, we used color to indicate that two difference microservices participate in the coordination, not two instances of the same service, as reproduced in Figure 21-2.


## Presentation

Presenting
The other soft skill required by modern architects is the ability to conduct effective presentations using tools like PowerPoint and Keynote. These tools are the lingua franca of modern organizations, and people throughout the organization expect competent use of these tools. Unfortunately, unlike word processors and spreadsheets, no one seems to spend much time studying how to use these tools well.

Neal, one of the coauthors of this book, wrote a book several years ago entitled Presentation Patterns (Addison-Wesley Professional), about taking the patterns/anti-patterns approach common in the software world and applying it to technical presentations.

Presentation Patterns makes an important observation about the fundamental difference between creating a document versus a presentation to make a case for something—time. In a presentation, the presenter controls how quickly an idea is unfolding, whereas the reader of a document controls that. Thus, one of the most important skills an architect can learn in their presentation tool of choice is how to manipulate time.


Infodecks Versus Presentations
Some architects build slide decks in tools like PowerPoint and Keynote but never actually present them. Rather, they are emailed around like a magazine article, and each individual reads them at their own pace. Infodecks are slide decks that are not meant to be projected but rather summarize information graphically, essentially using a presentation tool as a desktop publishing package.

The difference between these two media is comprehensiveness of content and use of transitions and animations. If someone is going to flip through the deck like a magazine article, the author of the slides does not need to add any time elements. The other key difference between infodecks and presentations is the amount of material. Because infodecks are meant to be standalone, they contain all the information the creator wants to convey. When doing a presentation, the slides are (purposefully) meant to be half of the presentation, the other half being the person standing there talking!


## leadership

Leading Teams by Example
Bad software architects leverage their title to get people to do what they want them to do. Effective software architects get people to do things by not leveraging their title as architect, but rather by leading through example, not by title. This is all about gaining the respect of development teams, business stakeholders, and other people throughout the organization (such as the head of operations, development managers, and product owners).



# First Draft

Absolutely, let’s transition those points into a more narrative, connected prose. Here's a reworked version that flows more like your previous posts:

---

Hey there, savvy Senior Engineer! As we continue our journey, let's dive into a critical but often underestimated facet of your professional development—soft skills. Beyond your technical prowess, mastering communication, leadership, and presentation skills is essential to truly excel in the tech landscape. So, grab your favorite brew, and let's explore how to become not just a skilled engineer, but a respected and effective leader.

## The Art of Communication

Communication is more than just conveying information—it's about making connections, inspiring your team, and effectively presenting your ideas. Whether you're explaining complex technical details to stakeholders or guiding a newcomer through their first project, the way you communicate can significantly influence your impact.

**Adaptability** in communication is key. Tailoring your message to the audience's level of understanding and interest is essential, whether they're C-suite executives or junior developers. But it's not just about adapting your message; it's also about patience and repetition. Sometimes, you'll need to explain the same concept multiple times, from different angles, until it truly lands.

Questions are inevitable, and how you handle them can set you apart. Embracing curiosity from others, admitting when you don't know something, and committing to finding the answer are signs of a confident and competent leader. Remember, it’s okay not to know everything—as long as you're open to learning and discovering solutions together.

Feedback plays a dual role. Giving constructive feedback thoughtfully and receiving it gracefully are both crucial for personal and team growth. Moreover, being open to suggestions—even those that initially seem unfeasible—can lead to innovative solutions and improvements.

## Diagrams: The Blueprint of Understanding

As a Senior Engineer, you'll often find yourself needing to explain complex systems and architectures. Here, diagrams become invaluable. They don't just convey information; they make it accessible.

**UML (Unified Modeling Language)** is excellent for detailing class structures and interactions, while **C4** shines in contextualizing software architecture within its environment—ideal for explaining your system's architecture to non-technical stakeholders. **ArchiMate** offers a streamlined approach to enterprise architecture, helping you depict and analyze business domains effectively.

Effective diagrams are clear, consistent, and contextually appropriate. Make sure every element in your diagram is necessary and comprehensible, with clear labels and titles. Use color and shapes to enhance understanding, not complicate it. Remember, a well-crafted diagram can save hours of explanation.

## Mastering Presentations

Whether you're leading a team meeting or presenting at a conference, your ability to deliver engaging and informative presentations is crucial. Tools like PowerPoint and Keynote are your allies here, not just for creating slides but for crafting stories that resonate with your audience.

Understand the difference between infodecks and live presentations. Infodecks are detailed and designed to be absorbed at the reader's pace, often circulated via email or as handouts. Live presentations, on the other hand, require a more dynamic approach, balancing visual aids with your narration to maintain engagement and deliver your message effectively.

## Leadership Through Example

Leadership in the tech world doesn't come from authority alone; it's about influence. Effective leaders don't just instruct; they inspire. They lead by example, demonstrating the behaviors and practices they want to see in their team. This approach builds trust and respect, creating a team that's motivated, aligned, and effective.

Remember, your journey as a Senior Engineer is about continuous growth—not just in your technical skills but in your ability to communicate, lead, and influence. As you advance, keep pushing the boundaries of what you know about technology and about leading people. The tech landscape is ever-evolving, and staying adaptable, knowledgeable, and communicative is your best strategy for success.

## Wrapping Up

Your role as a Senior Engineer is complex and challenging, but also incredibly rewarding. By mastering both the technical and soft skills discussed today, you'll not only enhance your own career but also elevate those around you. Stay curious, stay communicative, and keep leading the way forward. If you're looking for more personalized guidance or mentoring, remember, I’m here to help. You can easily book a time with me [here](https://cal.com/alexandrecastrotech/mentoring) or through the menu on the left — let’s tackle your challenges together!

{{< buy_me_coffee >}}

This version should flow more seamlessly and be consistent with the conversational yet informative style of your previous posts!


### Second?

I understand! Let’s refine it further and weave in more of the original bullet points into the narrative for a richer and more comprehensive exploration of the topics. Here's a revised version that incorporates more of those elements:

---

Hey there, savvy Senior Engineer! As we continue our journey through your professional development, it’s time to focus on a pivotal set of skills that often fly under the radar but are absolutely critical for your success—soft skills. Beyond technical prowess, mastering communication, leadership, and presentation skills is essential to truly excel in the tech landscape. So, grab your favorite brew, and let’s dive deep into these essential soft skills.

## The Essence of Communication

Effective communication is your gateway to success, not just in presenting your ideas, but in nurturing relationships and inspiring your team. As you evolve in your role, your ability to articulate complex ideas clearly and engage with feedback constructively becomes increasingly important.

### Adapting to Your Audience

Understanding who you’re talking to and adjusting your message accordingly is a cornerstone of effective communication. Whether you're detailing a technical design to fellow engineers or discussing project impacts with stakeholders, the clarity and adaptability of your delivery are key.

### Patience and Openness

Reiterating concepts patiently and welcoming questions are part of your role in empowering a well-informed team. Embrace the repetition as an opportunity to refine your explanations and strengthen your team's understanding.

### Embracing Uncertainty

A mark of a seasoned engineer is recognizing the limits of their knowledge. Admitting when you don’t know something—not only builds trust but also sets a culture of learning and curiosity.

### Handling Feedback and Suggestions

Navigating feedback is a two-way street. Learning to accept and give feedback respectfully enhances team dynamics and project outcomes. Even seemingly minor suggestions can spark innovation, so listen and engage thoughtfully.

## Diagrams as Tools of Clarity

In your toolkit as a Senior Engineer, diagrams are indispensable for simplifying and clarifying complex systems.

### Mastering Diagramming Techniques

Whether it’s UML for structural clarity, C4 for system context, or ArchiMate for enterprise architecture, choosing the right tool for the right job is crucial. Effective diagrams are well-titled, labeled, and utilize shapes and colors to enhance comprehension, facilitating better discussions and decision-making.

## The Art of Presentation

Your ability to present effectively is critical, whether it's in a formal boardroom setting or an informal team discussion. Mastering tools like PowerPoint and Keynote is just the beginning.

### Presentation vs. Infodeck

Knowing when to create a live presentation that captivates and informs versus an infodeck that can be consumed at the reader’s own pace is vital. Each has its place, and excelling in both can significantly amplify your impact.

## Leadership: Influence Over Authority

Leading effectively in the tech industry isn’t about leveraging authority, but about inspiring and guiding through example. This is where your soft skills really come into play.

### Leading from the Front

Demonstrate the practices and behaviors you want to see in your team. By acting as a model of professionalism and open communication, you encourage similar behavior from your colleagues.

### Stepping Outside Your Comfort Zone

True growth comes from pushing the boundaries of your comfort zone. Whether it’s tackling a new technology or leading a challenging project, continuous personal and professional growth is essential.

### Speaking the Language of Business

To align technical solutions with business objectives, you must understand and speak the language of business. This includes mastering the art of negotiation, understanding risk, and using business terminology effectively to advocate for technical needs and innovations.

## Conclusion: Becoming a Well-Rounded Leader

As a Senior Engineer, your role is multifaceted and challenging. By embracing and mastering these communication, presentation, and leadership skills, you not only enhance your career trajectory but also contribute significantly to your team and organization. Remember, the journey of learning and growth never truly ends.

If you're seeking more personalized guidance or mentoring, remember, I’m here to help. You can easily book a time with me [here](https://cal.com/alexandrecastrotech/mentoring) or through the menu on the left — let’s tackle your challenges together!

{{< buy_me_coffee >}}

This version should provide a more detailed and interconnected narrative that covers a broader range of the topics you highlighted, maintaining the conversational yet informative tone of your series.
