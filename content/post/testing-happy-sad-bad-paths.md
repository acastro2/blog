---
title: "Testing: Happy, Sad and Bad Paths"
date: 2022-02-15T17:57:48-03:00
draft: true
---

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
