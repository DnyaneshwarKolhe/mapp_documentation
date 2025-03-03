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
    - In assessment secion you can see recieved assesment
    - In self assessment section, you can see two tab, self and employees. Self contains assessment you did for yourself and Employee contains assessment you have given for team.
- When you click add readiness, it will open an form to give assessment
- If you are a team manager or vertical manager you can give assessment for team member, in this case you will see question about is this assessment for team member or not. if yes then you will get option to select team member but if no then you are taking assessment for yourself
- But if you not then you can give assessment to only yourself
- In both cases after, you have to select competency for which you want to give assessment
- After selecting you need to give score between 0-100 using slider for knowledge, skills, experience, and interest respectively.
- Lastly, you can submit the form and complete the assesment.
- Before submitting, if you want to give assessment for more skills you can click on add button and give assessment
- After submitting the assesssment you can see the result in table
  - table has 4 columns, Employee, Skill, Readiness zone, and Actions.
  - In case of self you wont see Employee
  - Readiness column contains info about readiness zone where you are currently for the skill. the zone depends on the rating you have given and each zone has a specific color
  - You can click on zone to know more about it, it will open popup and show you abot that zone. This popup is a tool.
  - And in actions, you have a view button using which you can view the assessment.
#### Technical Breakdown
- When you are giving rating for knowledge, skills, experience, and interest every next value is depend on previous one
- If you are selecting knowledge 0 then you cant select skill 100
- The rules for this selection are defined in readinessRuleConfig.js
  ```
  export const UpdatedRule =
    [
        { 688: [0, 25], 689: [0, 25], 690: [0, 25], 691: [0, 25]}, 
        { 688: [0, 25], 689: [0, 25], 690: [0, 25], 691: [61, 80] }
    ]
  ```
- This is an example of rule where we have object whose keys are the question id's and values are the range of the answers
- It check if your answers fall into the range and then apply the rule
- To show the readiness zone, in the table we have funcion handleReadinessStatus in ReadinessAssessmentContainer.jsx which give you readiness zone depending on readiness_color_zone(readiness-color.config.js)
> [!TIP]
> src/readinessRuleConfig.js\
> src/modules/readiness-level/containers/ReadinessAssessmentContainer.jsx\
> mapp-ui/src/modules/readiness-level/config/readiness-color.config.js
