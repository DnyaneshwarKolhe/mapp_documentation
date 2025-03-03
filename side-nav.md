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
