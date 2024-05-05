---
title: "Part 3: You are a Senior Engineer, Communication and other Soft Skills"
date: 2022-02-15T17:57:48-03:00
description: "This is a short description"
image: /media/author.png
draft: true
---

Find on that book the things about communication that they talk about, the software achitecture one.

Key pillar of good communciation:

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


## Testing Mermaid

### Flow Diagram

{{<mermaid>}}
graph LR;
   A[sheets ream<sup>-1</sup> <br> 500] -->|-1| B[thickness <br> 10<sup>-2</sup>cm <br>]
   C[thickness ream<sup>-1</sup> <br> 5cm] --> B
   B --> D[volume <br> 1cm<sup>3</sup>]
   E[height <br> 6cm] --> D
   F[width <br> 15cm] --> D
{{</mermaid>}}

{{<mermaid>}}
graph BT;
   A[Volume of Gold in Ring] -->|-1| B[Cost/Volume of Gold]
   I[Cost of Gold in Ring] --> B
{{</mermaid>}}

### Sequence Diagram

{{<mermaid>}}
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
{{</mermaid>}}

### Sequence Diagram

{{<mermaid>}}
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid
excludes weekdays 2014-01-10

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d
{{</mermaid>}}
