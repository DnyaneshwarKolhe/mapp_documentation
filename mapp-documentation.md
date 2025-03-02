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
- nivigation.js file contains object called bread_crums
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
#### User Guide
#### Technical Breakdown
### 1 on 1
#### Overview
#### User Guide
#### Technical Breakdown
### Feedback
#### Overview
#### User Guide
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
+ 
### Instruction for developers
+ Don't do a developement using super-user because backnd didn't check permissions for super-user but then for ther users it will throw and error
