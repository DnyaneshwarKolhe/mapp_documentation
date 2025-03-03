### Readiness Zone
#### Overview
- Readiness assessment allows employees and managers to evaluate skills.
- Two types of assessments:
  - Self-assessment (for individuals)
  - Team-assessment (for managers and vertical heads)
- Options available depend on user roles.
- Users select competencies and answer predefined questions.
#### User Guide
+ The first page contains
  - Add Readiness button to give assessment
  - Demo button to know more about the assessment
  - Table view for assessment and self-assessment
    - In the assessment section, you can see the received assessment
    - In the self-assessment section, you can see two tabs, self and employees. Self-contained assessment you did for yourself, and Employee contains the assessment you have given for the team.
- When you click add readiness, it will open a form to give an assessment
- If you are a team manager or vertical manager, you can assess a team member, in this case, you will see a question about whether this assessment is for a team member or not. If yes then you will get the option to select a team member, but if no, then you are taking the assessment for yourself
- But if you're not, then you can assess only yourself
- In both cases, after, you have to select the competency for which you want to give an assessment
- After selecting, you need to give a score between 0-100 using the slider for knowledge, skills, experience, and interest respectively.
- Lastly, you can submit the form and complete the assessment.
- Before submitting, if you want to assess more skills, you can click on the add button and give an assessment
- After submitting the assessment, you can see the result in the table
  - Table has 4 columns, Employee, Skill, Readiness zone, and Actions.
  - In case of self you won't see the Employee column.
  - Readiness column contains info about readiness zone where you are currently for the skill. The zone depends on the rating you have given, and each zone has a specific color
  - You can click on the zone to know more about it, it will open a popup and show you about that zone. This popup is a tool.
  - And in actions, you have a view button using which you can view the assessment.
#### Technical Breakdown
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
> [!TIP]
> src/readinessRuleConfig.js\
> src/modules/readiness-level/containers/ReadinessAssessmentContainer.jsx\
> mapp-ui/src/modules/readiness-level/config/readiness-color.config.js
