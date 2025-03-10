## Surveys
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
This document provides a detailed guide on the Survey Section within the application. The survey section allows users to create, manage, and analyze surveys, as well as handle survey tokens and invite participants for 360-degree surveys.
### User Guide
From this section we can see survey responses, create new surveys, manage tokens and invite 360 people \
This section has 5 sub-menus
  - **Response**: From here we can generate the survey responses and generate a survey report for the user
    - Here we get a search button to search the surveys by username, and list of surveys in the table
    - Table has Survey Name, Response Date, Response Duration, Action These columns and in Action we have a get report page which generates the report and sends it to the user's registered mail id
    - We can select the record from the table and then using the delete button above the table, we can delete it.
  - **Surveys**: Here we can create new surveys and edit or remove existing surveys
    - First we have **Add survey** button which opens a form to create a new survey
      - Here you need to fill in Name, Organizations, Active From, Shuffle, Report Query, Verticals, Teams, Active To, Public, Description and terms and condition, all these things, only the name is required thing in this
      - Active from and active to are the dates, and only in this duration the survey will be active
      - Public is a checkbox which decides if the survey will be available to use or not
      - Then you have the following buttons to save the survey
        - Save, which will save the data and take you back to the survey view 
        - Save and add another, The current Survey will be saved and a new form will be open to add a new Survey
        - Save and continue editing, The Survey will be saved but you will still be on the same page, so you can do further editing.
      - Then you have a search bar to search the survey, a reset button and a Delete button which is disabled.
      - Below, you can see a card, all the surveys are displayed here. The card contains the survey name, the action menu, the description, the public and shuffle toggle and the active till date.
        - the actions are Edit, delete and select
        - Edit will open the add form with info already filled to edit the survey.
        - Delete will remove the survey
        - Select will select the survey, which will enable the delete button, and we can delete the survey
      - When you click the survey, you can see survey information like name, description, active till, public and shuffle
        - You can see the edit button above, using which you can edit the survey
        - Then there is a survey assigned button, using which we can assign that survey to the organisation
        - **Groups:**
          - Before adding questions, a **survey group** must be created.
          - Groups have a **sequence number**, which determines their order in the survey.
          - Duplicate sequence numbers do not impact functionality but should be handled to avoid confusion.
          - The group have 3 actions using which we can add questions under that group, edit the group and delete the group
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
  - From here we can manage 360 takes
  - We have an option to single token, then multiple token, export token, edit or delete selected token
  - While adding token, survey, firstname, and lastname things are must, and email and mobile number are the optional things.
  - we can toggle invite, which will send the mail to the user after a token is generated
  - Below we can see all the tokens generated listed in the table
  - From the table view, we can select the token generated for a specific survey and delete or edit that token.
  - In a table, we also have an option to copy the link and send it manually to the user
- **360 survey**:
  - From this page we can invite people to give a survey
  - We can fill Employee, Survey Responses, and Message these fields in the form, but all of these fields are optional in the form section
  - In the to section we have E-mail, First Name, Mobile Number, Survey, Last Name, Response Type, these many fields out of which survey, first name and last name are required
  - You can clickthe  invite toggle to send an invite to the recipient and then submit to add a 360 invitation
