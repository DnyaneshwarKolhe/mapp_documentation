## Role definition
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview

### User guide
You can see following tabs n the role definition page. Its complete procedure from adding employee levels to assign roles in employee section.
  - **Employee Level**: Define the hierarchical levels within your organization (e.g., Junior, Mid-Level, Senior).
  - **Competency/ Sub-Competency**: Add competencies and sub-competencies, representing the key skills required for different roles.
  - **Role**: Create specific roles within the organization. Assign levels to each role and associate the relevant competencies.
  - **Job Family**: Group similar roles under a Job Family (e.g., Developer, HR, Research, Finance). This helps in better classification and career progression mapping.
  - **Threshold**: Define rating levels such as Poor, Good, Average, Excellent, used for performance assessment.
  - **Employee**: Here you can assign specific role to the developers of your organisation

This is only accessible for the CEO and POC only
#### Employee level
- Here on this page we can add multiple levels for the employee hirerchy
- The levels can be trainee, junior, mid, senior etc.
- In this page you will see
  - **+Add Level** *button*: using this button, you and add new employee level
    - It will open a popup where you can add title and description for the level
    - Title is compulsory and description is optional
    - If you enter a title which is already in use, It will show you an error(Employee level with same name already exist) while saving.
    - You you keep title empty and try to save, it will ask you to input title.
    - After addning correct things, you can either save it or cancel it.
    - Save will create new level and add it in table and cancel will discard the changes
  - **Table view of existing employee levels**: You can see all created levels here
    - Table have two columns, name and action, You can see level name under Name section
    - There is only delete action available in action column, using this you can delete the level.
    - Once you click delete, there is confirmation popup. you can confirm and delete the level
    - If description is added for any level, you can see arrow in front if level name using which you can see the description.
#### Competency
- The competencies are of two type
  - **Competency**: This competency, is like group of skills. We can list sub-competencies under compentencies.
  - **Sub-competency**: Sub-competencies are basically list of skills that employee needs to have in the organisation.
  - For example, competencies can be like Frontend and we can have sub-competencies which can fall under competency frontend like ReactJs, Javascript, typescript etc.
- When you hover over Competency tab, you can see button to select Sub-competency

**Competency tab**\
Here on this tab, you can see following component
  - **Add** *button*: This will open popup to add new competency which has Title, Plus button to add more, dropdown to select type and save and cancel button
    - You need to add unique title for the competency
    - Then select the type otherwies add button will be still diasbled 
    - Once you selected type, you can click add button to add multiple competencies under that type
    - Once done, You can either save which will create those competencies or you can cancel which will discard the changes.
  - **Import** *button*: If you have list of competencies in excel format, you can import that to create competencies.
    - This button will open the popup for importing file from where you can download templete or Upload the file
    - The templete have two columns, Title and competency type.
    - Once you uploaded file you can click import to create competencies or cancel to discard.
  - **Search bar**: Here, you can search the competencies, if you want to see any specific or you want to create new so to check if it is already exists.
  - **Competency table view**: In table, you can see the competency name, competency type, and actions to edit competency(Open same popup which we seen for add competency with values already added) and add sub competency(Open form to add sub-competency).

We are having two types of competencies, Generic and Functional which is role specific.

**Sub-competency tab**\
The componennts in both competency and sub-competency tab are same so we'll see onlly differences here\
list of components on these tab is as follows:
  - **Add** *button*: This will open form to add sub-competency, which consist of:
    - **Title**: Title of the sub-competency
    - **Competency**: Select the competency from the dropdown list 
    - **Type**: Once you select competency, this field will be auto populated, depending on the type of competency
    - **Description**: Not compulsory thing, you can add description about the skill if you want.
  - **Import** *button*: Same functionality only columns are title, description, competencyType and competency_category in which description is optional
  - **Search bar**: Same as competency
  - **Competency table view**: Same but added one extra column which is Competency between name and type. Add action changed to delete using which we can delete the sub competency.

This is all form this tab.
#### Role
Here in this tab you can Add new role, assign role to any employee or can edit or delete the existing role.\
The components of this page are as follows:
  - **Add** *button*: Open a form where you can add new role.
  - **Assign role** *button*: Open popup using which you can assign role to the employees
    - Popup have two select inputs, First one is to select employee and selcond one is to select role and level. Once selected you can save to assign role or cancel to discard the changes.
  - **Search bar**: You can search for specific role.
  - **Advance filter** *button*: This will add new select input below buttons to select education and year of experience.
  - **Role table view**: The table has 4 columns, Name(Role name), Level(Employee level for this role), Vertical and Actions which are
    - **View**: This will open detail page consist of
    - Role name, and edit, delete action
    - Details about employee level, created at, updated at, description, functional competency, responsibilities and eligibilities. You can see all available details here. 
    - You can click edit button, to edit the info. It will open same form which we used to add role with info already filled.
    - **Delete**: You can delete the role using this.

**Add role**

When you click add button, It will open form to add new role, the form contains
- **Title** *(Required)*: Title for the role
- **Description**: Description of the role
- **Select Level** *(Required)*: Select level from the employee level which we have added in Employee level section
- **Add button**: You can add employee level directly from here, if you dont have any or want to add new one.
- **Select vertical**: Here you can see list of verticals added to your organisation and you can select any one to assign this job role to that vertical.
- **Assign or add functional competency**: Here you have two option
  - Select the type of competency, can be either must have or good to have. If we select must have that user with this role muct have the competency/skills we selected
  - Select the sub-competency from the list of functional, The dropdown we are using is a custom made using which we can add new functional competency as well from here only
    - When you click add functional competency button the popup will be opened to add sub competency
    - Here we get option to between must have and good to have
    - Then add title of sub-competency
    - Select the competency under which this sub-competency fall, then you can add description which is optional and either save of discard.
    - Once you save, it will be added in the list of selected functional competency as well permenently added as sub competency in sub-competency list.
    - In this popup, you dont get option to add type of sub-competency since this popup is specifically for adding functional competency only so the type is by default functional competency.
- **Functional competency table view**: Here you can see all the sub-competencies added for this role
  - First column is function competency name, you can see arrow like icon in front of name if the competency has description. you can see the description by clicking the arrow.
  - Next column dont have name, in this column you can see if the sub-competency is must have of good to have in the form of toggle. You can also chnage it from here as well.
  - Last action is delete which do not delete the sub-competency actually but removes it from the selected sub-competencies list.
- **Select assiociated responsibilities**: Form here you select responsibilites associated with the role and if you dont find any then you can add it as well. If you click Add responsibility it will open popup where you need to add title and description(optional) and add the responsibility which will be added to selected responsibilities table as well.
- **Import button**: Here the popup to import is similler as other popup, the columns of excel are title and description. If you have excel of responsibilities releted to the role then you can directly import all of then using excel.
- **Associated responsible table view**: Same as functional competency teble where you can see name, description and perform delete action. You only dont have that must have and good to have toggle here
- **Add eligibility button**: Using this button you can add eligibility criteria for the role. This button will add form in same component which contains
  - Option to select if it is must have or good to have
  - Select the required education, if it is not listed, you can add using the button on the dropdown. Ao add new eduaction, you need to add stream, degree and subject from the popup and then save it.
  - Select required min and max experiance and then save it so it will be added as eligibility
  - you can add multiple eligiblilites and they will be visible in different table where
    - First row of table is detail about must have or good to have and buttons to edit and delete. Edit button open that add form again with the info already filled.
    - Second row is column header and third row in values. coulmns are, Required education, Specialisation, and Required Experience respectively
- **Save and cancel**: After filling all the required details you can save it to add new role or cancel to discard changes.
This is all about role tab.
#### Job Family
This section have three components
  - **Add job family**: This will open form consist of following sections to add job family:
    - **Title** *(Required)*: Add title of job family
    - **Description**: Description about the job family
    - **Add roles** *(Required)*: Roles which this job family includes. There is also add role button which will take you to the role section and open form to add role.
    - **Table view for roles added**: In table you can see Role name, Button to see description and delete action which will remove that role from the selected roles.
    - **Generic competencies**: Here you can select generic competency from the list of sub-competencies already added or click button on the dropdown itself which will open form to add generic sub-competency with fields title, competency, description and competency title and type you select other in competency. onc you added competency, it will get added to the table.
    - **Table view for generic competencies**: Same here like role table, you can see Role name, button to see description if available and delete button to remove the sub competency from the selected sub-competencies.
    - Save to create new job family with added details and cancel to discard the changes.
  - **Search bar**: You can search the job competency.
  - **Table view for job families**: The table has following columns
    - **Name**: You can see name of the job family.
    - **Role**: Here you can see no of roles added here. You can click the number to see the added roles in popup.
    - **Generic competency**: Here you can see no of generic competency added here. You can click the number to see the added generic competency in popup.
    - **Vertical**: Here you can see no of vertical added here. You can click the number to see the added vertical in popup. 
    - **Actions**: You have two action here
      - **View**: You can see the details for job family including name, created, updated, description, role, generic competencies and vartical
      - Also you can edit or delete job family using this page. edit will open same add form with values already added.
      - **Delete**: It will delete that perticuler job family.
#### Threshold
Here we add and rank criterias for the employees in organisation like Poor, Average, Good, Very good and Excellent.\
These threshold have only names so you cant add any description here. the page components are:
  - **Add threshold button**: This will add row in the table to add threshold, it has name filed and check and cross buttoon to save or discard.
    - You can type a name and either save or discard. once saved the row will be changed to non editable.
  - **Table view to add threshold**: Table will have name of the thresholds and delete and drag options using which you can delete the threshold or drag it to chnage the sequence.
#### Employee
This section have three main components:
- **Assign role button**: Open popup to assign role to the employees
  - First option is to select employees, you can select multiple empolyees
  - Second option is to select combination of role and level
  - Once you select, you can click save to assign role or cancel to discard the details.
- **Search bar**: You can search employees
- **Table view for employee**: Name, Level, Role these are the details available in table and you have delete Actions using which you can delete perticular role.

This is all about role definition
### Technical breakdown
- Navigations is being managed using localstorage, we are not chnaging UTL for this.
- The backend uses different naming conventions:
  - competency_category → Frontend refers to this as Competency
  - competency → Frontend refers to this as Sub-Competency
- Threshold management
  - Previously known as rating_scale, later renamed Threshold.
  - Uses Ant Design’s draggable table to allow drag-and-drop ordering.
  - Sequence-based ordering ensures the correct display of rating levels.
- Employee Role Assignment
  - The Employee Container handles role assignments.
  - GraphQL dynamic mutations determine whether to create or update role assignments.
  - If the employee already has a role, the system updates it; otherwise, a new record is created.
