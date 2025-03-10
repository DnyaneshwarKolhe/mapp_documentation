## Surveys
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
This document provides a detailed guide on the Survey Section within the application. The survey section allows users to create, manage, and analyze surveys, as well as handle survey tokens and invite participants for 360-degree surveys.
### User Guide
From this section we can see survey responses, create new surveys, manage tokens and invite 360 peoples\
This section have 5 sub-menus
  - **Response**: From Here we can generate the survey responses and generate survey report for the user
    - Here we get search button to search the surveys by username and list of surveys in the table
    - table has Survey Name, Respone Date, Response Duration, Action these columns and in action we have a get report page which generate the report and send it to the users registered mail id
    - We can select the record from the table and then using the delete button above the table, we can delete it.
  - **Surveys**: Here we can create new surveys and edit or remove existing surveys
    - First we have **Add survey** button which open a form to create new survey
      - Here you need to fill in Name, Organizations, Active From, Shuffle, Report Query, Verticals, Teams, Active To, Public, Description and terms and condition all these things only the name is required thing in this
      - Active from and active to are the dates, and only in this duration the survey will be active
      - Public is a checkbox which decides if the survey will be available to use or not
      - Then you have following buttons to save the survey
        - Save, which will save the data an take you back to the survey view 
        - Save and add another, The current Survey will be saved and new form will be open to add new Survey
        - Save and continue editing, The Survey will be saved but you will be still on same page, so you can do further editing.
      - Then you have search bar to search the survey, reset button and Delete button which is disabled.
      - Below, you can see card, all the surveys are displayed here. The card contains survey name, action menu, description public and shuffle toggle and active till date.
        - the actions are Edit, delete and select
        - Edit will open the add form with info already filled to edit the survey.
        - Delete will remove the survey
        - Select will select the survey which will enable delete button and we can delete the survey
      - When you click the survey, you can see survey iformation like name discription, active till, public and shuffle
        - You can see edit button above using which you can edit the survey
        - Then there is survey assigned button using which we can assign that survey to the organisation
        - **Groups:**
          - Before adding questions, a **survey group** must be created.
          - Groups have a **sequence number**, which determines their order in the survey.
          - Duplicate sequence numbers do not impact functionality but should be handled to avoid confusion.
          - Group have 3 actions using which we can add questions under that group, Edit the group and delete the group
        - **Questions:**
          - Each group contains **multiple questions**.
          - Supported question formats:
            - **Metric Survey**: Displays questions in a structured table format.
            - **Custom Survey**: Standard question format with multiple-choice options.
          - The **question order** is determined by the assigned sequence number.
          - **Choice Values:**
            - Each question has a set of predefined answers (checkbox, radio button, text input, etc.).
            - The value assigned to each choice determines how responses are recorded.
          - **Mandatory Questions:**
            - Certain questions can be marked as mandatory.
            - If marked, the user must answer before proceeding.
- **Tokens**:
  - From here we can manage 360 takens
  - We have option to single token, then multiple token, export token, Edit or deleteselected token
  - While adding token, survey, firstname and lastname things are must, and email and mobile no are the ooptional things.
  - we can toggle invite which will sent the mail to the user after token is generated
  - Below we can see all the tokens generated listed in the table
  - From the table view we can select the token generated for specific survey and delete or edit that token.
  - In table we also have a option to copy the link and send it manually to the user
- **360 survey**:
  - From this page we can invite people to give survey
  - We can fill Employee, Survey Responses, and Message these fileds in the for but all of these fields are optional in the from section
  - In the to section we have E-mail, First Name, Mobile Number, Survey, Last Name, Response Type these many fields out of which survey, firstname and lastname are required
  - you can click invite toggle to send invite to recipient and then submit to add 360 invitation
