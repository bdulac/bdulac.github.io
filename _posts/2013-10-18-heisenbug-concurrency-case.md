--- 
layout: post 
title: Heisenbug - Concurrency case 
categories:
  - Software quality
  - Heisenbug
  - Programming practice
  - UML
resource: true
---
<p>
	Solving an <a href="http://en.wikipedia.org/wiki/Heisenbug">Heisenbug</a>
	can be really tricky. This kind of bug occurs when the program
	execution conditions are changing. In many cases, using a <a
		href="http://en.wikipedia.org/wiki/Debugger">debugger</a> or a log
	output doesn't help. Such tools can have an influence on the execution.
</p>
<p>
	I once faced such a bug in a <a	href="http://en.wikipedia.org/wiki/Java_Swing">Swing</a> application. The problem occurred in a quite long process (half an hour)&nbsp; at various steps with constant input data. I lost time with that bug because I had no methodology. I have to admit the final solution was rather simple.
</p>
<p>
	I designed an <a href="http://en.wikipedia.org/wiki/Activity_diagram">activity diagram</a> of the main activities involved in the failing process. I paid attention to swimlanes because I suspected a concurrency problem. For each activity there was a single log output. A custom logging level was set up so that only activity logs could be written (an attempt with the debug log level was completely helpless). The logging framework was also configured to print the current thread name. There I got the activity which was not in the right place and the name of the criminal. The random occurrence of the problem was probably due to the variable system load and user interactions.
</p>