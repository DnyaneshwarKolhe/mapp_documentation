## POC Dashboard
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
The POC Dashboard provides an overview of key organizational data, including employee levels, team structures, analytics, licensing, and reports. The dashboard is structured to fetch, process, and display critical data using GraphQL queries, JavaScript functions, and chart visualization components.
### User Guide
The POC dashboard mainly consists of 4 sections, which give us information like the organisation overview, Licensing and a Graphical representation of survey assessment status.
#### Organisation overview
- This section is the first row of the page
- Here we can see statistics of the organisation in the card format
- First card is **Total verticals**, This will show the count of total verticals in the organisation.
- Second card is **Total teams**, Here we can see the total number of teams in our organisation.
- Third card is **Total managers**, Here we can see how many managers are there in our organisation. It includes the CEO, the Vertical Head, and Team managers. 
- Last card is **Total Employee**, The count of all remaining employees is displayed here. If the POC is a manager or vertical head, then he is considered in total managers, otherwise he will be counted here.
#### Analytics
- The first section of the second row is analytics, here we can see the percentage of out of all employees how may employees are using each module.
- First is general analytics and below that you can see the Modules used from most to least.
- The data is displayed in the circular progress bar, where the percentage is written in it and you can see the module name and count of employees using out of all employees in the card format.
- You can click the card, which will take you to the detail page. Where the first generic one opens the Mapp overview, and if you click the module specific card, it will take you to the module usage page with the desired module selected.

**Mapp Overview**: 
- In this page we can see all the details in the table format. There are three columns as follows:
- First column is module name, here we can see a list of all the modules in the application.
- Then in the next column, which is "no. of employee", we can see the count of employees which are using these modules.
- And last column is usage, which tells you the percentage with progress bar about the number of employees using the module out of a total number of employees. 

**Module Usage**: 

In this page, we can see all the details in the table format.

At the top of the page, we can see three things
  - First is drop-down to select the module, from here we can switch between modules
  - Second is the search bar, using which you can search for the statistics for the particular employee.
  - And the last one is filers, we have All, 1 Year, 6 Months, 30 Days, 7 Days, and 24 Hours, these many filters using which we can see data for desired duration.

Then we have a table as follows
- We can see the Employee name in the first column, then the next columns are the submodules under that module we have selected to see details, and last accessed date in the last column.

- **The table content varies between the SOUL module and other modules:**
  - In **SOUL**, the system checks whether the corresponding survey has been completed. If it has not, a **pending icon** is displayed to indicate incomplete status.
  - In **other modules**, the table displays the **count of specific user actions**, such as feedback given/received, IDPs created, and completed activities.
  - The **first and last columns remain consistent across all modules**:
    - The **first column** displays the employee's name.
    - The **last column** shows the date of the most recent action recorded within that module.

Here is the list of all the columns in each module
- **Soul**: Employee Name, Values, Strength, Personality, Knowledge & skills, Impact narrative, Last Accessed Date
- **IDP**: Employee Name, Total IDP, Completed, Inprogress, Pending, Revised, Drafted, Last Accessed Date
- **OKR**: Employee Name, Total OKR, Created OKR, Assigned OKR, Collaborated OKR, Accepted OKR, Last Accessed Date
- **Readiness zone**: Employee Name, Self Assessments, Received Assessments, Last Accessed Date
- **Feedback**: Employee Name, Feedback Given, Feedback Received, Last Accessed Date
- **Coaching conversation**: Employee Name, Total Coaching engagements, Completed, In Progress, Last Accessed Date
- **Kudos**: Employee Name, Issued Badge, Received badge, Last Accessed Date
- **1:1 Meeting** Employee Name, Total 1 on 1, Completed, Upcoming, Last Accessed Date
#### Licencing
The second section of the second row is the Licensing section, which has two cards
- In the first one, we can see the total licenses, used licenses and their representation as a progress bar
- Used licenses include a total number of active uses and the invited users. It does not include the past users who are removed from the organisation.
- Second one is the button to Invite employees to the organisation
  - It open form which is like table to add the details of the employees and invite them to the organisation.
  - Vertical, Team, Email, First Name, Last Name, and Position, these are the details required in the form, where you can select vertical, then select team(you will not be able to select it before selecting vertical)
  - Fill the rest of the things and select any one of the Vertical head, manager and employee from the position section.
  - You can see the cross button next to the last role input using which you can delete the row and add button below the table which adds new row to the table to invite more employees
  - You can invite a maximum of 10 employees at a time.
  - Lastly, you can click cancel to discard the changes or click invite to invite all the added employees.
#### Survey Assessment Status
- The third and last section is the Survey Assessment Status section, where we can see a dropdown to select the survey and a graphical representation of the survey.
- Graph is a horizontal bar chart, on one side of the graph, we can see a list of all Verticals and teams and a percentage on the other side.
- You can click any of the bars which will take you to the detail page.

**Detail Page**:
- Here on the detail page, you can see a dropdown on the left from where you can select the vertical and export button on the right.
- Export button will open a popup where you can select the vertical and team and then export the data.
- Below that, you have another dropdown at the right which allows you to switch between surveys.
- Then you have a graph which shows the percentage of employees for each team, how many employees have completed the survey and the below graph, you can see the survey completion status of the entire vertical.
- You can click on the team bar in the chart, which will show the details of employees from that team in the table below.
- Next section is a table where we can see the employees from the  vertical and team
- If you have clicked on the team bar in the chart, then you will be able to see the employees from the team only, but if not, then you can see the details of all the employees in that vertical
- The table shows Employee, Team, Response date, Status, and Actions, and you can see a checkbox before the employee name who hasn't completed the survey. You can click individual or click select all to select all the employees who have not completed the survey, and click send reminder to send reminders to all of them.
### Technical Breakdown
- For export functionality, we have a function called exportToCsv which is written in functions.js
- This is a common function and we are using it in the entire application.
- It accepts two parameters, the First one is filename, and the second is data.
- For the 360 invite reminder functionality, we are using dynamic mutation.
- The table in which we are showing data, is a common table(tableView.jsx).

> [!TIP]\
> src/modules/look/components/functions.js
> src/modules/poc-dashboard/components/common/tableView.jsx
