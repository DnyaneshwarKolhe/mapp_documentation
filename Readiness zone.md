## Readiness Zone
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
- Readiness assessment allows employees and managers to evaluate skills.
- Two types of assessments:
  - Self-assessment (for individuals)
  - Team-assessment (for managers and vertical heads)
- Options available depend on user roles.
- Users select competencies and answer predefined questions.
### User Guide
+ The first page contains
  - Add Readiness button to give assessment
  - Demo button to know more about the assessment
  - Table view for assessment and self-assessment
    - In the assessment section, you can see the received assessment
    - In the self-assessment section, you can see two tabs, self and employees. Self-contained assessment you did for yourself, and the Employee contains the assessment you have given for the team.
- When you click add readiness, it will open a form to give an assessment
- If you are a team manager or vertical manager, you can assess a team member, in this case, you will see a question about whether this assessment is for a team member or not. If yes, then you will get the option to select a team member, but if no, then you are taking the assessment for yourself only.
- But if you are not a team manager or vertical manager, then you can assess only self
- In both cases, after, you have to select the competency for which you want to give an assessment
- After selecting, you need to give a score between 0-100 using the slider for knowledge, skills, experience, and interest respectively.
- When you are giving a rating for knowledge, skills, experience, and interest, every next value depends on the previous one
- If you are selecting knowledge 0, then you can't select skill 100
- Lastly, you can submit the form and complete the assessment.
- Before submitting, if you want to assess more skills, you can click on the add button and give an assessment
- After submitting the assessment, you can see the result in the table
  - Table has 4 columns, Employee, Skill, Readiness zone, and Actions.
  - In case of self, you won't see the Employee column.
  - Readiness column contains info about readiness zone where you are currently for the skill. The zone depends on the rating you have given, and each zone has a specific color(blue, orange, red, green, purple)
  - You can click on the zone to know more about it.
  - And in actions, you have a view button using which you can view the readiness zone popup which show information about that zone. This popup is a tool, and there are different popups for the different zone. We can edit the content of these popups from the superuser tool section.
  - This popup also has edit and delete action, using which you can edit or delete the readiness assessment.
  - Pop-up contains videos, which have info about the zone and actions to take.
### Technical Breakdown
- When you are giving a rating for knowledge, skills, experience, and interest, every next value depends on the previous one
- If you are selecting knowledge 0, then you can't select skill 100
- The rules for this selection are defined in readinessRuleConfig.js
  ```
  export const UpdatedRule =
    [
        { 688: [0, 25], 689: [0, 25], 690: [0, 25], 691: [0, 25]}, 
        { 688: [0, 25], 689: [0, 25], 690: [0, 25], 691: [61, 80] }
    ]
  ```
- This is an example of a rule where we have an object whose keys are the question IDs and values are the range of the answers
- It checks if your answers fall into the range and then applies the rule
- To show the readiness zone, in the table we have the function handleReadinessStatus in ReadinessAssessmentContainer.jsx, which gives you the readiness zone depending on the readiness_color_zone(readiness-color.config.js)
- The readiness_color_zone is an array of objects, each representing one zone and having a set of rules.
- We are looping over the user's response, then validating it with rules and adding it in an object with the zone and the question ID alongside status.
- Once we checked for all rules, we checked for all entries of the object and found out a key for which the value is true.
- After we again check for that zone id in readiness_color_zone and get the correct zone for the user's response.

> [!TIP]
> src/readinessRuleConfig.js\
> src/modules/readiness-level/containers/ReadinessAssessmentContainer.jsx\
> mapp-ui/src/modules/readiness-level/config/readiness-color.config.js
