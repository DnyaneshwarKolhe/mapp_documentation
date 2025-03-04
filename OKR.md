## OKR
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
---
The **OKR** (Objectives and Key Results) module is designed to help users set, track, and manage their objectives and key results within an organization. The module allows users to create objectives, define key results, assign tasks, collaborate with team members, and track progress through milestones. The module is structured to ensure clarity and accountability in achieving organizational goals.
### User Guide
---
- The okr module have 3 tabs
  - **Objective key result**: To view and manage objectives, key results and milestones
  - **Dashboard**: To view collective data for all objectives, like progress and all
  - **Request**: To view and manage all assignment and collaboration requests
- We have tool button on side wich contains more information about OKR
- The hirarchy of OKR is like first we have Objective, under objective we can add Key result and Under key result we add milestone.

We'll see seeting things in detail in next chapters
#### Objective key results
- These modules have following components
  - **ADD OKR** *Button*: This will add new row in the table to add OKR
  - **Date filter**: We can select date range to filter out and see OKR's in the selected date range only
  - **Search bar**: We can also search perticular OKR from the list
  - **OKR table view**: When user click ADD OKR the new row will be added here. And we can see list of all OKR's and key results and milestone. the table have 4 columns, objective, Due Date, Owner(s), Progress.
- The process for adding OKR, Key result and milestone is as follows.
  - Click on **ADD OKR**, It will add row in table where you need to Objective, and Due Date and then click save to create OKR. Owner and progress is disabled while creating Objective.
  - Now your OKR is created, and you can see owner, setting icon to add the weightage, progress bar and menu icon at the end. the menu icon will have following options
    - **View** This will open details page for corrousponding Objective/KR/milestone.
      - In objective detail page, we can do following things: discard, delete, add KR, add weight and extend correction deadline
      - In KR detail page everything is similler except we get option to add competency and add milestone instead of add okr
      - And in Milestone detail page, we get options to discard, delete, and extend correction deadline
    - **Cascade**: This will open a popup which has tree like structure of the the OKR
      - In tree, each node is card, you might see card which is not expanded but if you click it, it will expand
      - Each card contains label, then profile icon, username, progress and button for child, if its Objctive, button is KR. If its kr button is milestone.
      - If you click button inside of the card, popup will open showing info about childs, there progress, who are they belongs to etc.
      - The nodes are connected by lines, and the line color is depending upon the type of linking, for Objective its green, Blue for the KR and orange for the milestone
      - The selected card will have green border which indicates the selection
    - **Edit**: We can edit the OKR using this, but this button is disabled in following scenarios
      - Due date is passed
      - Correction deadline is passed
      - If you're not owner, means if it is assigned or if its collaborated.
    - **Kudos**
    - **Discard**: Using this, you can raise the discard request to the manager, if case if plan changed and you are not working on that feature anymore or you dont want to work on it. once you raise discard request the color fo thatrow will turn blue from green and once approved it will turn into black.
    - **Delete**: You can delete the OKR using this within correction deadline.
  - There is arrow like icon at the start, if you click that, now row will be added to add key result in a tree structure.
  - Similler to Objective you need to fill the info and save it, and the key result will be created.
  - Once KR is created, instead of setting icon, you can see icon to update progress. and also you can see one multi-user like icon in the Owner section to assign or collaborate. Here are 3 possible scenarios
    - First you create milestone and Own Key result for yourself.
      - In that case you can add milestone if the task is bigger or directly update the progress.
      - If you add the milestone, the KR logo of adding progress will change to setting logo to change weightage and this is same for all cases of creating milestone.
    - You can collaborate with your team member, distribute weightage.
      - Your team member will recieve the collaboration request
      - You can create milestone for the KR or update the progress directly on KR
    - You can assign the KR to your team member, after that you wont be able to add milestone under it. The KR will become objective of your team member.
#### Dashboard
- On dashboard firstly you can see OKR progress average in row for
  - **My OKR**: Available for everyone
  - **Team**: Visible to team manager
  - **Vertical**: Visible to vertical head
  - **Organisation**: Visible to the POC admin
- All thses cards have percentage of completion. And the cards like team, vertical have arrow button to switch between teams if the user is part of multiple teams or verticals
- Below that we have cascaded and non-cascaded objection represented by doughnut chart, with different status like Missed, In progress, Pending, completed and discarded
  - **Cascaded Objective**: The objective which someone else have created and assigned or collaborated with you
  - **Non-cascaded Objective**: The objective which you have created for yourself
- we show these doughnut chart are depending on the card selected above, it we select for team we can see team details and same for the organisation and vertical.
- Below that we have two section which are depends on the card selected above
  - If **My OKR** card is selected
    - First section contains **Upcomming milestone**
    - Second section is **My Okr Performance**
  - If **Team** Card is selected
    - First section is team or members performance represented by horizontal bar chart
    - Second is list of team member with completed percentage
  - If **vertical** card is selected
    - First section is vertical or team performance represented by horizontal bar chart
    - Second is list of sub-verticals and teams
  - If **Organisation** card is selected
    - First section is Organisation or vertical performance represented by horizontal bar chart
    - Second is list of verticals alongside with percentage
- In all above cases except My OKR, If you click the item from the list of second section, It will open the popup where performance is represented  as Horizontal bar chart in left side and as doughnut chart in left side
- If the bar is about OKR, you can see green arrow in front of it which will take you to that perticular OKR
#### Requests
- This is a dropdown with 3 options
  - **Assignment**: here you will see Assignement requests in the table. You can view the request in detail view and then either accept the request or Disscuss about the request by creating instand or scheduled one on one. there is also option to see details about thet Objective.
  - **Collaboration**: here you will see Collaboration requests in the table. You can view the request in detail view and then either accept the request or Disscuss about the request by creating instand or scheduled one on one. there is also option to see details about thet Objective.
  - **Discard**: And here you can see any discard request raised
### Technical Breakdown
---
#### Doughnut chart
- The doughnut chart is from the library called chart.js you can find its documentation [here](https://www.chartjs.org/)
- Whenever you need to add or change somting check the version we are using and change it accordingly in documentation to refer.
- The options of doughnut chart are as follows
  responsive: Ensures the chart resizes when the window is resized.
  - maintainAspectRatio: Maintains the original aspect ratio of the chart.
  - animation: Disables the animation duration for the chart.
  - plugins-> legend:
    - display: Hides the legend.
    - title: Displays the title of the legend with padding.
    - labels: Uses point style for the legend labels with a specific box width and font size.
    - position: Positions the legend at the bottom of the chart.
  - tooltip -> callbacks->  label: Customizes the tooltip label to show the percentage and count of each segment. For the 'Pending' label, it also shows discard and contribution requests.

#### Horizontal Bar chart
- This chart is custom made since we want to show progress inside the bar only and also want to show label above the bar
- Since this functionality is not available in chart js bar chart we craeted owr custom
- You can find out this bar char in PerformanceBar.jsx
#### Cascade tree
- To show this we are using library called react-d3-tree
- Tree component requires following properties
  - **key**: A unique identifier for the tree instance.
  - **data**: The data to be visualized in the tree structure. the data of structure can be as follows.
    ```
    {
      "name": "Objective 1",
      "attributes": {
        "owner": "John Doe",
        "progress": "50%",
        "type": "Objective"
      },
      "children": [
        {
          "name": "Key Result 1",
          "attributes": {
            "owner": "Jane Smith",
            "progress": "75%",
            "type": "Key Result"
          },
          "children": [
            {
              "name": "Milestone 1",
              "attributes": {
                "owner": "Alice Johnson",
                "progress": "100%",
                "type": "Milestone"
              }
            },
            {
              "name": "Milestone 2",
              "attributes": {
                "owner": "Bob Brown",
                "progress": "60%",
                "type": "Milestone"
              }
            }
          ]
        },
        {
          "name": "Key Result 2",
          "attributes": {
            "owner": "Charlie Davis",
            "progress": "40%",
            "type": "Key Result"
          }
        }
      ]
    }
    ```
  - **orientation**: Sets the orientation of the tree. In this case, it is set to "vertical".
  - **zoom**: Sets the initial zoom level of the tree.
  - **renderCustomNodeElement**: A custom function to render the nodes of the tree, we can customise default nodes.
  - **translate**: Sets the initial translation (position) of the tree.
  - **separation**: Defines the separation between sibling and non-sibling nodes.
  - **nodeSize**: Sets the size of each node in the tree.
  - **collapsible**: Determines whether nodes can be collapsed or not.
  - **dimensions**: Sets the dimensions of the tree container.
  - **pathClassFunc**: A custom function to set the class for the paths connecting nodes. here we are checking the type of node and then returning a dynamic classed to customising the lines accordingly
- you can find this code in ObjectiveTreeView.jsx file
> [!TIP]
> src/modules/look-v2/Components/PerformanceBar.jsx\
> src/modules/Objective-keyresult/components/ObjectiveTreeView.jsx
