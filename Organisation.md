## Organisations
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
### User Guide
- Here, in this page, you have invite employees button and two tabs below that.
- To invite employee we should have atleast one vertical under the organisation otherwise the button will be disabled.
- **Process to invbite employee**:
  - It open form which is like table to add the details of the employees and invite them to the organisation.
  - Vertical, Team, Email, First Name, Last Name, and Position these are the details required except team in the form, where you can select vertical, then select team(you will not be able so select it before selecting vertical)
  - Fill the rest of the things and select any one of the Vertical head, manager and employee from the position section.
  - You can see cross button next to last role input using which ypu can delete the row and add button below the table which adds new row to the table to invite more employees
  - You can invite maximum 10 employess at a time.
  - Lastly, you can click cancel to discard the changes or click invite to invite all the added employees.
  - After inviting, these employees will be added as non-varified employees in the orgnisation.
- The tabs are as follows:
  - **Organisation tree**: Here you can see and edit all the employees in the organisation in the form of tree.
  - **All employee**: Here you can see all the employees in the table.
#### Organisation tree
- This tab has three buttons and tree
- **Recenter**: This button will take to to the organisation in tree
- **View Mode**: This is the default mode in which the tree id initially shown.
  - Here in this mode, you can see the organisation first and then at nect level, you can see the verticals in card format.
  - Card have vertical names, then vertical manager name if available, totle employee count in that vertical and lastly no of teams/ sub-vrticals under that vertical.
  - The no of teams or sub-verticals are shown in specific color and when you click that box of count, the next level of tree will be open which represents the sub vertical or vertical in the form of branch of tree.
  - The cards are same for vertical, sub-vertical and team. only if the vertical, subvertical dont have child like team in both and sub-vertical under vertical, then the box with count is not visible there.
  - The organisation as well as the cards in the tree have menu button(three dots), you can click that to see the details about either organisation or vertical, sub-vertical and team
    - If you click to view the details of organisation, the popup will open which have organisation name and list of POC and CEO in the organisation.
    - In other cases, You can see the name of vertical, team or sub vertical, Name of the respective person like vertical head, manager or sub vertical head and list off all employees on the popup. you can also search the employees using the search bar given
- **Edit mode**: Here you can edit the tree, add vertical, sub vertical and teams.
  - When you click edit mode, it will open organisation tree with all the nodes are expanded.
  - Same as view mode first is organisation which has menu icon(...), using which you can see the details of the organisation same as view mode.
  - The rest of the cards are also similler to view more but you can see the no of sub-vertical or teams since all the nodes are already expanded.
  - We can also click on card which will add new nodes from which we can select type of node, and give name it will create the card for that name.
  - All cards have menu, like view mode but here we get two option extra. We have details which works similler but apart from that, we also have Edit and Delete actions.
    - Edit will open the popup where we get 3 things, we can change vertical/ sub-vertical/ team name, you can change or add more vertical heads and add or remove employees.
    - To add employee or manager here, they should be part of an organisation.
    - You can delete the team, sub-vertical and vertical but if you deleting vertical, or sub-vertical all the teams/sub-vertical under that vertical or sub-vertical will get deleted.
#### All employees
- When you g to all employees section, the filter button will be added next to the search bar using which we can filter the employees by vertical, position and status
- If you click of any of the vertical then you can also get option to filter it using teams under that vertical.
- The all employees tab have followings components
  - **Create vertical button**: We can create the vertical using this
    - Here, The popup will be opened where vertical name is mandatory.
    - Then we get toggle to switch between teams and sub-vertical and get the button to add sub vertical.
    - If we click add team or sub-vertical,the input box appear where we can input the sub-vertical or team name
    - We can add multiple sub-vertical and teams
  - **Export button**:It will export all the employees data from the organisation, but wont include the removed employees in it.
  - **Employee Table**:
    - **Employee**: First column, you can see the name of the employees here and status ofbthe employee is displayed before employee name as icon. If employee if verified you you can see blue check icon but if he is not, you can see red cross.
    - **Position**: Position of employee like CEO, POC Admin, Vertical head, Team manager and Employee
    - **Vertical**: You can see the vartical names user added in. It could br empty or we can on have one or more verticals added here depends on the no of vertical user is part of.
    - **Status**: It is either active or in active
    - **Team**: If the user is part of any teams, those teams will be listed here.
    - Then we can see (...) menu next to teams which has 3 actions
      - **Edit**: We can edit the employees using this
      - **Deactivate**: We can deactivate the users so they will be temperorily suspended, We can activate them leter. You can see warning popup and once you confirm the user will be deactivated and Deactivate button will be changed to **Activate**. Deactivating will not reduce the licence count
      - **Remove Employee**: Re can remove the employee from the organisation, Once removed we cant add same employee again. It will also remove one licence from the used one.
      - We cant Deactivate or remove other POC and CEO
### Technical Breakdown
- While removing employees, we dont remove them completely from the DB, Instead we add exit date so if we need to have functionality like past employees we can have that.
- To show the tree we are using library called react-d3-tree
- To decide the color of node, we are having key called node type which can be team, vertical, sub-vertical.
- When you click the node in edit mode and it is showing option which nodes can be created, the type of that node is CREATE_CHOICE_NODE
- In some cases like verified/non-verified, we dont have specific key to identify in the data but we have filters using which we can get verified and non verified get under separate keys using aliasing.
- In table, we sort data according to the employees position and then show in order from CEO to Employee.
#### User creation steps
User Creation
  - When a new user is created, they are first added to the user table.
  - Backend automatically creates an entry for the user in the profile table.
  - The frontend does not need to handle this profile creation explicitly.
Employee Creation
  - Once the user ID is obtained, the user must be added to the employee model.
  - The addEmployeeMutation is used to convert a user into an employee.
  - This step is essential before assigning them to an organization.
  - If any errors occur during employee creation, those users are filtered out.

Assigning Employee to an Organization
  - After creating an employee, they must be assigned to an organization.
  - The createMemberMutation is used for this.
  - operation type: createMember
  - related type: organization ID

Assigning Employee to a Vertical or Team
  - If the user is assigned as a vertical head:
  - They are added to the organization first.
  - Then they are assigned to the vertical using createMemberMutation with vertical ID.
  - If the user is assigned as a team member:
  - They are added to the organization.
  - Then they are assigned to the team using createMemberMutation with team ID.
  - If the user is a team manager:
  - They are added to the team as a team manager instead of a regular employee.
