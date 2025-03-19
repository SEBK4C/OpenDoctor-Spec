# OpenDoctor-Spec
Open Doctor = Like _Cursor.sh IDE but for medical history_

Open Doctor Spec- _Cursor IDE but for medical history_
---
(what is in scope?)

The 
- System is Fully portable:
- Patient data File system:
- Database schema: 
- LLM server stack, as packaged single binary:
  
Background processes:
- permissions, file system traversal and file Edit APIs and Multi Database scheduler:
  
Front end: (exactly like Cursor Coding tool but for medical documents)
---
-  Right side collapsible File system view: 
- Middle view: Date scroll with text summary of Medical timeline (Oldest Medical documents at the bottom of the timeline.) newest documents at the top.  
	- Scroll the timeline past the TOP of "timeline" (Scroll with inertia animation) 
		- Snap page Too a "State of health one pager" with prominent (Export as PDF button.)
- Left Side: Vertical Split in the window Chat conversations and horizontally split bottom "Autonomous diagnosis - Smart Forms View". 
	- This is the primary AI interaction point. 
	- patient can ask questions of their own medical data with a RAG pipeline that scrolls to the correct point in their history. And let them have a conversation about details within that data..
	- from this conversation, transcript symptoms and medical interventions can be inferred. Then A form will be generated, asking the user if the symptoms/medication/historical-dates are accurate and if they would like the system AI to add it to their timeline. (The user has easy selection to correct any inaccurate information within the Smart-Form directly.) 
	- When a "Smart form" is submitted, a summary is generated on the Timeline at the appropriate date range and a new GIT commit is made.  (Allowing the user to roll back to previous versions of their medical history. Keeping a detailed file versioning system available for historical medical intervention references.)
	![[Screenshot 2025-03-19 at 08.53.37.png]]
---
Developer tools:
---
- Open Doctor LLM agent runtime MAKER: 
	- Packages Open Doctor agent dependencies into a single binary and Hashes the resulting file. 
- Medical-qualifications Permission assigner. 
	- Provides an AI  "Open Dr ranking" 
	- Registers model "qualifications" with background scheduler and tool database.
- 
----
Standards:
---
- We publish "Known Good"  medical AI standards for agents interactions with patients and doctors. 
	- Patient interactions : User query Conversations, AI intake form and patient query, History tracking and "Medical timeline",  state of patient "one pager".
	- Doctor interactions : Knowledge query Conversations,  Histories "Medical timelines",  state of patient "one pager".

- Benchmarks standards
	- "medical-qualifications" tests
- safety standards
	- patient data permissions (API-tool_use-level 1,2,3,4...)
	- patient conversation permissions  (AI_level 1,2,3,4...)
	- hallucination detection (big Brother)
	- Data change tracking and immutability (Git)
- API standards.. 
	- how to request a database permission, 
	- how to build new Open Dr. runtimes with your specific tools.
-  "Known Good LLM agent runtimes", compiled binaries and signed.
	- How to publish those runtimes so others can use them
