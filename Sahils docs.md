

# Dashboard, Side Nav, and Soul Module Documentation
## KT GIVER: , KT RECIEVER:

## Overview
This document provides a detailed explanation of the **Dashboard**, **Side Nav**, and **Soul** modules, including permissions, GraphQL queries, coding practices, and module-specific workflows.

---

## Side Nav Module

### Side-Nav.jsx
- **Purpose**: Contains all the values for the sidebar that can be changed dynamically from within the file.
- **Dynamic Configuration**: Adjust sidebar items directly in the file to reflect changes in the UI.

---

## Dashboard Module

### Permissions
- **Dashboard Access**: Accessible to everyone without specific permissions.
- **Feedback Permission**: Required to show the feedback button.
- **OKR Permission**: Required to show OKR-related features.
- **Coaching Engagement Permission**: Required to show coaching engagement features.

#### Path to Change Permissions
- Go to `src -> permissions -> userdashboardpermissions` to adjust the permissions of the modules for the dashboard.

### Dynamic Team Listing
- **Team Manager**: Fetches and lists teams managed by the user.
- **API Call**: `Team Manager Employee` to get the list of teams.

### GraphQL Queries
- **Fetching Teams**: Use `Team Manager Employee` API to get teams managed by the user.
- **Fetching Survey Responses**: Use `Survey Responses` API to check if a user has completed a survey.
- **Fetching Meetings**: Use `All Meetings` query to get upcoming meetings.

### UI Adjustments
- **Icon Positioning**: Adjust the position of icons to avoid UI distortion.
- **Permissions Handling**: Show or hide UI elements based on user permissions.

---

## Soul Module

The **Soul** module is the core of the application, designed to help users reflect on their values, strengths, and impact. Initially, the CDD team conducted **Soul Hackathons** onsite, but as the user base grew, **Learning Paths** were introduced to streamline the process.

### Learning Path
- **Purpose**: A list of videos and instructions to guide users through their Soul Surveys.
- **Static Data**: Data shown in static pages of the Soul module is stored in `homePageContent[type]`.

### Ways to Provide Soul Survey Values
1. **Take the Survey**: Users can take the survey to provide values.
2. **Top 5 Values**: If users already know their values, they can directly enter their top 5 values.

### Impact Narrative
The **Impact Narrative** module allows users to reflect on and share their impact within the system. Initially, users entered their own narratives, but it was later transitioned to an AI-based system.

#### Key Concepts
- **impactnarrativeset**: This query gives the total count of times a user has taken an Impact Narrative.
- **Flow of Impact Narrative**:
  1. Fetch the user's impact narrative.
  2. If there are no results (`edges` is zero), no data is displayed.
  3. If any values are missing or the backend fails, the user is given the option to regenerate the narrative.

#### AI-Generated Impact Narrative
- **RunPod Integration**: The AI for generating the Impact Narrative runs on **RunPod**.
- **Worker Availability**: Before assigning the task, the system checks the RunPod health to ensure workers are available. If no workers are free, the request is either queued or rejected.
- **Regeneration**:
  - Users can regenerate their Impact Narrative if they’ve made changes to their survey.
  - Regeneration is only allowed after completing all Soul Surveys.

### GraphQL Aliases
- **Purpose**: GraphQL's alias feature allows the same operation to be executed multiple times in one HTTP request by attributing a name (alias) to each result.
- **Usage in Impact Narrative**: Used to generate all values in one request.

#### Example Query
```graphql
query {
  values: surveyResponses(surveyId: "values", last: 1) {
    responseDate
  }
  strength: surveyResponses(surveyId: "strength", last: 1) {
    responseDate
  }
  personality: surveyResponses(surveyId: "personality", last: 1) {
    responseDate
  }
}
```

### Soul Identity
- **Purpose**: Displays the list of values from the Soul Surveys.
- **Manager Access**: Managers can view the Soul Identity of their employees.

---

## Employee Data Structure

The **Employee Object** contains various fields related to the user's involvement in different organizations and roles:

- **Id**: Unique identifier for the employee.
- **OrganizationSet**: Total count of organizations the person is part of.
- **OrgPocEmployee**: Count if the user is a POC (Point of Contact) for any organization.
- **OrgCeoEmployee**: Count if the user is the CEO of any organization.
- **VerticalHeadEmployee**: Count of the number of verticals the user is a head of (manager role).
- **VerticalMemberEmployee**: Count of verticals the user is a member of (non-manager role).

### Definitions
- **Vertical Member Employee**: Gives the count of verticals the user is a part of.
- **Team Member Employee**: Provides a count of how many organizations the user is a member of but not a manager.

---

## Development Best Practices

1. **Requirements Definition**: Always define requirements before starting development to avoid wasting time or resources.
2. **Function Reusability**: Keep functions separate for reusability.
3. **Intervals and Timeouts**: Clear intervals and timeouts on component unmount to prevent memory leaks.
4. **Date Handling**: Use `moment-timezone` for consistent date handling across the application.
5. **Code Reusability**: Encapsulate reusable logic in separate functions.

### Example Code Snippets

#### Fetching Survey Responses with Aliasing
```graphql
query {
  values: surveyResponses(surveyId: "values", last: 1) {
    responseDate
  }
  strength: surveyResponses(surveyId: "strength", last: 1) {
    responseDate
  }
  personality: surveyResponses(surveyId: "personality", last: 1) {
    responseDate
  }
}
```

#### Clearing Intervals on Component Unmount
```javascript
useEffect(() => {
  const interval = setInterval(() => {
    checkRunpodHealth();
  }, 300000); // 5 minutes

  return () => clearInterval(interval);
}, []);
```

#### Moment.js Date Comparison
```javascript
import moment from 'moment-timezone';

const isAfter = moment(responseDate).isAfter(impactDate);
if (isAfter) {
  setRegenerateButton(true);
}
```

---

## Conclusion
This documentation covers the key aspects of the **Dashboard**, **Side Nav**, and **Soul** modules, including permissions, GraphQL queries, coding best practices, and module-specific workflows. Following these guidelines will ensure a consistent and efficient development process.
```

This combined `.md` file provides a comprehensive overview of all the discussed topics, making it easier for the team to reference and implement the features and practices.
