# MApp- Manager Awesomeness App
### Table of Content
- [Navigations](#navigations)
  - [Navbar](#navbar)
  - [Navbar- Super user](#navbar--super-user)
  - [Navbar- Notifications](#navbar--notifications)
  - [Navbar- My account](#navbar--my-account)
  - [Navbar- Organisations](#navbar--organisations)
  - [Navbar- Mapp support](#navbar--mapp-support)
  - [Side-nav](#side-nav)
- [Home](#home)
  - [Dashboard](#dashboard)
  - [My Team](#my-team)
- [Soul](#soul)
  - [Learning Path](#learning-path)
  - [Values](#values)
  - [Strengths](#strengths)
  - [Personalities](#personalities)
  - [Knowledge & Skills](#knowledge--skills)
  - [Impact Narrative](#impact-narrative)
  - [Soul Identity](#soul-identity)
- [Role](#role)
  - [OKR](#okr)
  - [Readiness Zone](#readiness-zone)
  - [1 on 1](#1-on-1)
  - [Feedback](#feedback)
  - [Coaching Engagement](#coaching-engagement)
  - [Managing Performance](#managing-performance)
  - [IDP](#idp)
- [Shoal](#shoal)
  - [3C](#3c)
  - [User Manual](#user-manual)
  - [Team Dynamics](#team-dynamics)
- [Whole](#whole)
- [Poll](#poll)
- [Survey](#survey)
  - [Survey List](#survey-list)
  - [Report](#report)
- [Kudos](#kudos)
- [HR](#hr)
  - [BARS](#bars)
  - [Role Definition](#role-definition)
  - [Role Relation](#role-relation)
  - [Hiring](#hiring)
- [Admin](#admin)
  - [POC Dashboard](#poc-dashboard)
  - [Organization](#organization)
  - [Reports](#reports)
  - [Token](#token)
## Navigations
#### Overview
### Navbar
#### Overview
- Its very simple module with Application logo, Page title, Breadcrum(optional in some page) and other icons
- Other icons includes:
  - **Super-user icon**: Only people with superuser access will be able to see that. we'll see about this in details in upcomming chapters
  - **Notification**: __in_progress
  - **FAQ**: __in_progress
  - **My account**: this section contains info about user profile, notification settings, tips settings and reset password. We'll see about this section in details in upcomming chapters.
  - **Organisations**: __in_progress
  - **Mapp support**: __in_progress
#### Technical Breakdown
- navigation.js file contains object called bread_crums
  ```
  export const bread_crums = [
    {
      path:home_route.employee_profile,
      crums:["Employee Detail"],
      check_param:false
    },
    {
      path:`${okr_route.discardRequest}?tab=collaboration`,
      crums:["Request","Collaboration Request"],
      check_param:true
    }
  ]
  ```
- this object contains path, array or crums which are being shown when user visited that path and check_params
- side-nav.jsx file has function which check for that path and render the bread-crums accordingly
### Navbar- Super user
### Navbar- My account
### Navbar- Organisations
### Navbar- Mapp support
### Side-nav
#### Overview
Side-nav contains list of all modules and submodules. It help user so quickly navigate through the modules
#### User Guide
- In side-nav we have two side-navigation bars.
- one is for the modules and another one is for the submodules
- Whenever user select any module, It will be highlited in green color
- There are some modules as well as sub modules which are not developed yet, we are showing toast msg as **Feature coming soon**
#### Technical Breakdown
- We have navigations.js file which contains object of modules and submodules
  ```
    export const navigations = [
      {
        key: home,
        title: "Home",
        path:home_route?.userdashboard,
        icon: navigationIcons.home_icon,
        menu_type:menu_type?.normal,
        module_name:module_config.home,
        child: [
          {
            key: dashboard,
            title: "Dashboard",
            icon: navigationIcons.dasboard_non_active,
            icon_active: navigationIcons.dasboard_active,
            path: home_route?.userdashboard,
            menu_type:menu_type?.normal,
            module_name:module_config.dashboard,
          },
          {
            key: my_team,
            title: "My Team",
            alternative_title:"My Team Dashboard",
            icon: navigationIcons.teams_non_active,
            icon_active: navigationIcons.teams_active,
            path: home_route?.my_team,
            menu_type:menu_type?.normal,
            module_name:module_config.my_team,
            arrow_icon:navigationIcons?.nav_drop,
            is_expand:true
          },
        ],
      }
    ]
  ```
- In this above example, all things are pretty much straight forward, the navigations is an array of object
- each object represent the module and the **childs** inside the object is a list of sub-modules.
- Here are the rest of the properties of the navigation object
  - **key**: the key is unique and the background selection depending on the key
  - **title**: the title is shown on the UI in sidebar as well as in navbar
  - **alternative_title**: its optional thing, it can be used in case where we want to show different title in navbar, so the title willl be appear in sidebar and alternative_title will be appear on navbar
  - **path**: used to navigate on click
  - **icon**: icon for that module or sub-module
  - **menu_type**: Each menu object has a menu type; it can be normal, survey or tool. If the menu type is survey, we must add two more properties. 
    + **Survey_id**: Specify which survey to show 
    + **Check**: This is a flag that indicates if we want to check if the survey is completed or not. If the survey is completed, then we can decide if we want it to navigate to the survey report page; otherwise, only the survey page is shown.
  - **module_name**: the module_name property can be used in future to show or hide specific modules only. 
    - If you go to settings under organisations in the Django admin, we can create settings. We have three options to create settings
      - **Org**: Select organization for which you wanna add settings
      - **Ui Cfg**: Here, mention the module that you wanna show or hide
      - **Status**: It can be either true or false; if anyone is true, the user will be able to see only those modules that have status true for that organisation; otherwise, if it’s false, the user will see all the modules except those that are false 
  - **is_expand**: Some side-bar menu can have dropdown as well so this will set true in such cases, like under _my team_ we can have multiple teams then we can have a dropdown there to select team
  - **arrow_icon**: if the is_expand is true, we need to give arrow icon to show the dropdown
  - **icon_active**: 
  - **is_coming_soon**: if this is true, then we show that toast message: **Feature comming Soon**
- side-nav.jsx takes this navigation object and render it to show sidebar
- There are few modules which are not for all the users, so in side-nav.jsx, we have a function called custom permissions.
- This function check if user is manager, or CEO or POC and then and only then allow user to view those modules or sub-modules
> [!TIP]
> navigations.js: src/modules/layout/navigations.js\
> side-nav.jsx: mapp-ui/src/modules/layout/side-nav.jsx
## Home
#### Overview
### Dashboard
#### Overview
#### User Guide
#### Technical Breakdown
### My Team
#### Overview
#### User Guide
#### Technical Breakdown
## Soul
#### Overview
### Learning Path
#### Overview
#### User Guide
#### Technical Breakdown
### Values
#### Overview
#### User Guide
#### Technical Breakdown
### Strengths
#### Overview
#### User Guide
#### Technical Breakdown
### Personalities
#### Overview
#### User Guide
#### Technical Breakdown
### Knowledge & Skills
#### Overview
#### User Guide
#### Technical Breakdown
### Impact Narrative
#### Overview
#### User Guide
#### Technical Breakdown
### Soul Identity
#### Overview
#### User Guide
#### Technical Breakdown
## Role
#### Overview
### OKR
#### Overview
#### User Guide
#### Technical Breakdown
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
### 1 on 1
#### Overview
#### User Guide
#### Technical Breakdown
### Feedback
#### Overview
- The Feedback module allows users to submit, receive, and manage feedback within the system.
- It includes features such as:
  - Motivational and Developmental feedback
  - Kudos integration
  - Filters and search functionality
  - Custom feedback types and validation
#### User Guide
- The feedback page has following component
- **Give feedback button**: This will open form to give feedback. Feedback form includes the following fields
  - There are two types of feedback you can give
    - **Motivational/Recognition**: This feedback is given when we want to praise someone for there work or learnings etc.
    - **Developmental/Constructive**: If we found that someone is lacking in there skills/ work or they need to work on some part then in that case we can give this feedback.
  - Then we need to select Recipient, who is going to recieve that feedback
  - Once we select feedback there is on button called OKR, If you have to give feedback related to any perticular OKR then you can click that button and you will get option to select OKR added by corrusponding person.
  - If you are giving Motivational feedback you can see option to give Kudos, this option is hidden in case of Developemental feedback.
  - Then we have claps module using which you can give feedback step by step
    - C - Create Safety by stating how the feedback will help the receiver.
    - L - Lay out context by referring to a specific situation, so the feedback is not generalized.
    - A - Articulate behavioral evidence by describing actions / speech objectively and without personal opinions.
    - P - Probe for possible alternatives that the receiver can try to act on the feedback.
    - S - Support for next steps and commitments by offering help, advice and by being an accountability partner.
  - P is suggestation for the reciver about things he can try for imporvement so it can given in case on developemental feedback only
  - There is also one more toggle called detailed, if you enable it you can see separate inputs instead of single description box.
  - When you details for all module in claps, you can review and submit feedback.
- **Demo button**: Upon click, this button will show video about how to give feedback
- **Tool button**: This contains additional information about giving feedback
- **Tablist for Submitted, Recieved and feedback**
- **Quick Links section**
#### Technical Breakdown
### Coaching Engagement
#### Overview
#### User Guide
#### Technical Breakdown
### Managing Performance
#### Overview
#### User Guide
#### Technical Breakdown
### IDP
#### Overview
#### User Guide
#### Technical Breakdown
## Shoal
#### Overview
### 3C
#### Overview
#### User Guide
#### Technical Breakdown
### User Manual
#### Overview
#### User Guide
#### Technical Breakdown
### Team Dynamics
#### Overview
#### User Guide
#### Technical Breakdown
## Whole
#### Overview
## Poll
#### Overview
## Survey
#### Overview
### Survey List
#### Overview
#### User Guide
#### Technical Breakdown
### Report
#### Overview
#### User Guide
#### Technical Breakdown
## Kudos
#### Overview
## HR
#### Overview
### BARS
#### Overview
#### User Guide
#### Technical Breakdown
### Role Definition
#### Overview
#### User Guide
#### Technical Breakdown
### Role Relation
#### Overview
#### User Guide
#### Technical Breakdown
### Hiring
#### Overview
#### User Guide
#### Technical Breakdown
## Admin
#### Overview
### POC Dashboard
#### Overview
#### User Guide
#### Technical Breakdown
### Organization
#### Overview
#### User Guide
#### Technical Breakdown
### Reports
#### Overview
#### User Guide
#### Technical Breakdown
### Token
#### Overview
#### User Guide
#### Technical Breakdown
## Permissions, Routing and Best coding practices
### Permissions
+ Each module or functionality requires some specific set of permissions.  
+ The permissions are actually implemented in backend, whenever we try to fetch some data, it will check for the permissions for that module, if its given we’ll receive the data but if it is not then the UI will break 
+ So, to prevent the UI from breaking, we are adding those permissions in by creating a new file in the permissions folder for that module. 
+ Before rendering the data, we’ll check for permission. If permissions are there, we’ll show the module; otherwise, we will not. 
#### Process to add permissions: 
+ If you are working on a new module, create the file for that module under the permissions folder; otherwise, look for the existing file. 
`
/Users/dnyaneshwar/Work/mapp-ui/src/Permissions/oneonone.permission.js
`
+ Like this, now we will have a permanent object there, required_permission, which holds all the permission required for that module in the form of array. 
+ If that module has any other dependent permissions from another module, like run pod for tips or feedback if we have feedback button, so we can import those permissions from respective modules. 
+ Now, In the UI code file, we have one predefined function called globalPermissionValidator, which takes two arguments. 
  + The first one is module permission to validate  
  + The second one is all user permissions 

It will return objects with the same keys but different values. If all permissions match, it will be true; if any permission doesn’t match, it will be false 
### Routing
+ We have created one method: navigateRoute, which we should use to navigate instead of using useHistory.
+ So in future, if we go for library upgrade and the methods are changed, then we can change it on one place only, and It can be applied automatically throughout. 
### Best coding practices
#### Rendering tablist
```
let tab_list = {
        assessments:{
            key: 'assessments',
            label: 'Assessments',
        },
        self_assessments:{
            key: 'self_assessments',
            label: 'Self Assessments',
        }
    }
    
    const [current_tab, setCurrentTab] = React.useState(
        tab_list[match?.params?.type] ||
        {
            key: 'assessments',
            label: 'Assessments',
        }
    )
  
    const views = {
        assessments: ReadinessAssessmentContainer,
        self_assessments: SelfReadinessAssessmentMainView,
    }
    const CurrentView = views[current_tab?.key]
```
- Here we have an object called tablist which contains list of tabs.
- And we have views which contains components for different tabs
- When tab changes, we are setting state variable and depending on that the view will be selected and stored in CurrentView
- So by only rendering CurrentView, we can render all tabs, we dont need to compare and render every components for the tabs like
```
current_tab === "assessments" && <ReadinessAssessmentContainer />
```
### Instruction for developers
+ Don't do a developement using super-user because backnd didn't check permissions for super-user but then for ther users it will throw and error.
### Graphql
#### Dynamic queries 
- mapp-ui/src/modules/readiness-level/containers/AddReadinessContainer.jsx
