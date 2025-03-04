## Feedback
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
The **Individual Development Plan** (IDP) module is designed to help employees take ownership of their personal and professional growth. Unlike the **Coaching Engagement** module, where a manager defines improvement areas for their reportees, the IDP focuses on self-initiated skill development and career progression.
With the IDP module, employees can:
- Identify and plan their skill development areas.
- Set personal learning goals and milestones.
- Track progress over time in a structured manner.
- Take proactive steps towards career advancement and competency improvement.

By using this module, individuals can create a clear roadmap for their growth, ensuring they develop the skills and competencies needed for their current role or future aspirations.
### User Guide
- In IDP module, you can see the following components
  - **New IDP** *button*: You can create a new IDP by clicking this button
  - **Team IDP** *button*: If you are a Manager, Vertical head, POC or CEO, then and only then you can see this button to view your team's TDP
  - **Demo** *button*: This opens a demo video about how to use IDP 
  - **Search bar**: You can search specific IDP using the search bar.
  - **IDP table view**: Here you can see a list of the IDP. The columns are as follows:
    - **My Goals**: This is the goal title
    - **Manager**: You can see your manager here
    - **Completion Status**: It can be To do, Draft, In Progress, Approved, Pending, Completed and Revised.
    - **Milestone**: Then you have a date of the milestone here
    - **Actions**: You can perform two actions on the IDP, Edit and Delete. You can only edit the IDP before approval, once approved, you can not edit it.
#### New IDP
- When you click **New IDP**, it will open form to create new IDP
- In that form, you have to select a type of IDP if it is short term or long term
- Then you need to fill out the following fields
  - **Goal**: Add a goal for which you are creating IDP
  - **Skills**: Select skills from the list of sub-competencies
  - **Developmental Activities**: Add what all activities you are going to do for personal development. You can add a step-by-step process that you will follow
  - **Next milestone**: Here you need to figure out what milestone would be and select the date by when we will complete that milestone
  - **Resources**: Here you can list all resources you need  to achieve the goal
  - **Current Reporting and Mentoring Manager**: If you have a manager assigned, then you can see it here, otherwise you can add one who will approve the IDP
  - **Actions**: You can click Submit to save it or Save draft to save it as draft for now and then update it in future.
#### IDP table view
- When you create the IDP, it will go to your manager for review at that time the IDP status will be pending.
- Manager can either approve if he finds everything good, otherwise give suggestions. So if he approves the status, it will be Approved, or if he suggested some changes, then the status will be revised
- Once approved you can go to detail page and change the completion status to To Do, In progress or Completed.
- When you click on the IDP, you can see the IDP details at left, and Created date, Status(Pending or Approved only) and comments(if any) on the right side.
- If the milestone is already passed and IDP is still pending, then in that case you will get an option to update the milestone date from the details page itself.
#### My team(For Team manager, Vertical head, POC or CEO)
- Here you can see two sections
  - **Request**: Here you can see all the request you have to act on, or your team member raised for the approval but For now all the IDP's are shown here irrespective of status.
  - **Employee IDP Status**: All the IDPs of your team member are listed here irrespective of status.
### Technical Breakdown
- All the status of IDP are listed in a config file(idp.config.js)
- After fetching data, we check for the status of IDPs, If we found any which is In Progress  we'll show tip regarding if not then we'll check for pending and follow the same process, and same for revised as well.
- We are caching the tips, and check for the scenario after 1 hr and then show the tip again. You can change cache time from config.js(ai_tip_cached_hour)
- To show the Team IDP, we are fetching managers permissions in IdpHomeContainer.jsx
- We have a query called direct manager, using which we can fetch the direct manager of the user
- Also, when a user has some information added in IDP and change the IDP type from lets say short term to long term, the data will be preserved and added there as well.
- When we open a popup for selecting manager, we are fetching employees who are either Manager, Vertical head, POC or CEO and show them in the popup. And if we select other, then we get an input box to add the email of the manager
- We are having a more type pagination where we check the end cursor and then fetch the data
  - First time we don't send end cursor since we are fetching  first 10
  - On every API call, we receive the end cursor which holds the ID of the last record
  - For every next record we are passing this end cursor to fetch the record next to that.

>[!TIP]
> src/modules/IDP/idp.config.js\
> src/modules/IDP/containers/IdpHomeContainer.jsx

