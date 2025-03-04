## Feedback
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
The **Individual Development Plan** (IDP) module is designed to help employees take ownership of their personal and professional growth. Unlike the **Coaching Engagement** module, where a manager defines improvement areas for their reportees, the IDP focuses on self-initiated skill development and career progression.
With the IDP module, employees can:
- Identify and plan their own skill development areas.
- Set personal learning goals and milestones.
- Track progress over time in a structured manner.
- Take proactive steps towards career advancement and competency improvement.

By using this module, individuals can create a clear roadmap for their growth, ensuring they develop the skills and competencies needed for their current role or future aspirations.
### User Guide
- I IDP module you can see following components
  - **New IDP** *button*: You can create new IDP by clicking this button
  - **Team IDP** *button*: If you are manager, Vartical head, POC or CEO then and only then you can see this button to view your teams TDP
  - **Demo** *button*: This opens a demo video about how to use IDP 
  - **Search bar**: You can search specific IDP using the search bar.
  - **IDP table view**: Here you can see list of the IDP. The columns are as follows:
    - **My Goals**: This is the goal title
    - **Manager**: You can see your manager here
    - **Completion Status**: It can be To do, Draft, In Progress, Approved, Pending, Completed and Revised.
    - **Milestone**: Then you have date of the milestone hare
    - **Actions**: You can perform two actions on the IDP, Edit and Delete. You can only edit the IDP before approval, once approved, you can not edit it.
#### New IDP
- When you click **New IDP**, it will open form to create new IDP
- In that form you have to select type of IDP if it is short term or long term
- Then you need to fill following field's
  - **Goal**: Add a goal for which you are creating IDP
  - **Skills**: Select skills from the list of sub-competencies
  - **Developemental Activities**: Add what all activities you are going to do for personal developement. You can add step by step activities
  - **Next milestone**: Here you need to figure out what milestone would be and the select the date by when we will complete that milestone
  - **Resources**: Here you can list all resources you need  to achieve the goal
  - **Current Reporting and Mentoring Manager**: If you have manager assigned, then you can see it here otherwies you can add one who will approve the IDP
  - **Actions**: You can click Submit to save it or Save draft to save it as draft for now and then update it in future.
#### IDP table view
- When you create the IDP, it will go to your manager for review at that time the IDP status will be pending.
- Manager can eiter Approve if he find everyting good otherwise give suggestation. So if he approves the status will be Approved or if he suggested some changes then status will be revised
- Once approved you can go to detail page and change the completion status to To Do, In progress or Completed.
- When you click on the IDP, you can see the IDP details at left, and Created date, Status(Pending or Approved only) and comments(if any) on the right side.
- If the milestone is laready passed and IDP is still pending then in that case you will get option to update the milestone date from the details page itself.
#### My team(For Team manager, Vertical head, POC or CEO)
- Here you can see two section
  - **Request**: Here you can see all the request you have to act on, or your team member raised for the approval but For now all the IDP's are shown here irrespective of status.
  - **Employee IDP Status**: All the IDP's of your team member are listed here irrespective of status.
### Technical Breakdown
- All the status of IDP are listed in a config file(idp.config.js)
- After fetching data, we check for the status of IDPs, If we found any which is In Progress  we'll show tip regarding if not then we'll check for pending and follow the same process, and same for revised as well.
- We are chaching the tips, and check for the scenario after 1 hr and then show the tip again. You can change cache time from config.js(ai_tip_cached_hour)
- To show the Team IDP, we are fetching managers permissions in IdpHomeContainer.jsx
- We have query called direct manager using which we can fetch direct manager of the user
- Also when user has some information added in IDP and chnage the IDP type from lets say short term to long term, the data will be preserved and added there as well.
- When we open popup for selecting manager, we are fetching employees which are either Manager, Vertical head, POC or CEO and show them in the popup. and if we select other, then we get input box to add email of the manager
- We are having show more type pagination where we check of the end cursor and then fetch the data
  - First time we dont send end curser since we are fetching  first 10
  - On every API call, we recieve the end cursor which holds the ID of last record
  - For every next record we are passing this end cursor to fetch record nect to that.

>[!TIP]
> src/modules/IDP/idp.config.js\
> src/modules/IDP/containers/IdpHomeContainer.jsx

