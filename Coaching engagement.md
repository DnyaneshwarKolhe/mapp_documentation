## Coaching Engagement
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
The Coaching Conversation module facilitates structured learning and mentorship within an organization. It enables senior employees or managers (coaches) to guide junior employees or peers (coachees) in improving specific skills or competencies. The module provides a step-by-step framework for conducting coaching sessions and tracking progress.
### User guide
- This page has the following components
  - **New engagement button**: You can create new coaching engagement
  - **Demo button**: Demo video to understand the working of the module
  - **Search bar**: Search any specific coaching engagement
  - **Table view of coaching engagement**: Here, you can see all previous coaching engagements. You can be a coach or coachee. Click any engagement to see the details.
- The name of the survey is grow, because it's known as a grow previously, later it changed to coaching conversation, but in the  backend and the UI codebase, it's still known as grow
#### Adding new engagement
- When you click the button to add a new coaching engagement, a form will open
- Here firstly you need to select a coachee
- Then you can select what this conversation is related to based on that, you get an option to select
  - **OKR**: If you select OKR, then you will get a list of that person's OKRs, whom you selected as coachee
  - **Skill**: If you believe he lacks proficiency in any specific skill area, you can choose from a list of skills. Once you make a selection, you will be presented with a variety of sub-competencies related to those skills, allowing you to further refine your assessment
- Then we need to select clarify goal and add its description
- Next option is you need to rate your coachee on a scale of 1-10 for that OKR or skill, and below that you need to add a description of the reason behind the rating
- Then you need to add what all things are not working and what are the challenges the coachee would like to discuss.
- After we need to add what coachee can do to address the top challenges and how commmited the coachee feel to this idea.
- Lastly, we can plan the next steps, by when, and what the coachee needs from you(the coach), by what date. We get the option to add more rows for adding next steps and things needed by coachee.
- We can select the date when we should follow up again and then submit the form
- This page also contains a Tool icon which will show more info about the survey.
#### Engagement table view/ Engagement board
- Here you can find a list of engagements in the form of a table
- Table has 3 columns, Name, Coachee's goal statement and follow-up on
- In the name section, you can find the role below the name, this table holds all the engagements like someone coaching you or you coaching someone.
- So the role will be like My Coach or My Coachee
- You can click on any element from the list to view the details page for that engagement.
- In the details page, if you are a coach, you can change the status of the next step to be done, but if you are a coachee, you can't see the next step on the details page. You have an option to update the progress of assistance needed.
- You can chnage the status according to the progress, Status are Not started, In progress, Facing challenges, Discarded, Completed and unsuccessful.
- When you change the status of the next step of assistance needed, the icon will be changed according to the status.
- Once you moved it to the completed status, you will not be able to change the status again
- We'll get an option to add a change this status for all next step as well as Assistance needed as per your role.
- And at the end of the page, Coach has two buttons, next conversation to add new conversation and cancel to go back to list view, whereas Coachee has only the cancel button to go back
### Technical breakdown
- While fetching the data, do separate coach and coachee, we are using aliasing
- We are passing the current user and fetching the record in which the user role is either coach or coaching, there is no filter at the backend side, so we use aliasing
- In future thre can be multiple surveys for coaching engagement, if different organisations want different set of questions. To identify the survey, we are adding the survey identifier in the config.js file to get the survey details using that identifier.
- For the skill dropdown, we have created a custom dropdown component since we have to add options on the dropdown to add skills(SkillField.jsx).
- CreateConversationView.jsx: Here in this file, we are passing data to the SinglePageQuizView component, which will map over the questions and render the survey accordingly using the component 
> [!TIP]
> There are two conditions to view the survey
> + You should have permission to view, otherwise you will get an error permission page
> + You can get an error permission page even if you have permission, the survey is not public
>
> This is not a survey, that's why it's not listed under survey module, but the backend considers it as survey. This same case is with feedback and readiness as well.\
> src/modules/grow-model/components/CreateConversationView.jsx\
> src/modules/survey/components/SinglePageQuizView.jsx\
> src/modules/survey/components\SinglePageSectionComponent.jsx\
> src/modules/look/components/form-components/SkillField.jsx
