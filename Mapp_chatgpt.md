# Knowledge Transfer (KT) Documentation - Day 1

## Table of Contents
- [Introduction](#introduction)
- [Dashboard Overview](#dashboard-overview)
- [Navigation System](#navigation-system)
- [Sidebar Components](#sidebar-components)
- [Permissions System](#permissions-system)
- [Bread Crumbs and UI Elements](#bread-crumbs-and-ui-elements)
- [React Navigation Changes](#react-navigation-changes)
- [Survey Handling and Conditional Navigation](#survey-handling-and-conditional-navigation)
- [Configuration-Based UI Rendering](#configuration-based-ui-rendering)
- [Module-Based UI Restrictions](#module-based-ui-restrictions)
- [Handling Data in Local Storage](#handling-data-in-local-storage)
- [Use of Object Entries, Keys, and Values](#use-of-object-entries-keys-and-values)
- [Performance Considerations with `every` and `some`](#performance-considerations-with-every-and-some)
- [Conclusion](#conclusion)

---

## Introduction
This document provides a detailed explanation of the technical and theoretical aspects covered in the Day 1 Knowledge Transfer (KT) session. It includes insights into the dashboard functionality, navigation handling, permission management, UI configurations, and code-level implementations.

## Dashboard Overview
The dashboard consists of multiple components and navigation menus:
- Various widgets and panels
- Conditional rendering based on user roles
- Navigation elements embedded within the dashboard
- Specific navigations triggered by clicks on dashboard elements (e.g., clicking on "Employee" navigates to the employee profile section)

## Navigation System
Navigation is dynamically controlled based on the URL state.
- No explicit state management is used for navigation highlighting.
- Active menu items are determined based on the URL structure.
- Example: `role/feedback` auto-selects "Role" and "Feedback" in the sidebar.
- The key must match the first part of the URL to ensure highlighting.

### Code Structure
```javascript
const navigation = [
  {
    key: 'dashboard',
    title: 'Dashboard',
    path: '/home/dashboard',
  },
  {
    key: 'role',
    title: 'Role Management',
    path: '/role',
    children: [
      { key: 'feedback', title: 'Feedback', path: '/role/feedback' },
    ],
  },
];
```

## Sidebar Components
### Navigation Mechanism
- The sidebar is built using `SideNav.js`.
- Parent and child items are managed dynamically.
- The key must match the first part of the URL to ensure highlighting.

### Role-Based Sidebar Adjustments
- `my team` section is shown only for `Team Managers`.
- `HR` section is visible only for specific roles.
- Some options in the sidebar are dependent on organization-level settings.

### Conditional Sidebar Display
- A setting allows an organization to restrict the visibility of certain modules.
- If no restrictions are applied, all modules are displayed.
- Example: If `soul` is set to `true`, only `soul` is displayed, and all others are hidden.

## Permissions System
- Permissions are validated both on the frontend and backend.
- Backend permissions are checked automatically unless the user is a super admin.
- Permissions are stored in local storage for quick access.
- Uses `getPermission` function to fetch all necessary permissions.
- Every module has its required and optional permissions.

### Fetching Permissions
```javascript
const getUserPermissions = async () => {
  const response = await fetch('/api/permissions');
  return response.json();
};
```

## Bread Crumbs and UI Elements
- Breadcrumbs are dynamically generated based on navigation.
- Uses a mapping system to render titles based on URLs.
- Alternative titles can be configured to show different labels in the sidebar versus the page title.

```javascript
const breadcrumbs = [
  { path: '/dashboard', label: 'Dashboard' },
  { path: '/employee/profile', label: 'Employee Profile' },
];
```

## React Navigation Changes
- Transition from `history.push` to `useNavigate` in React 18.
- Encapsulated navigation logic for future-proofing.
- A global `navigateRoute` function is used to centralize navigation logic.
- This approach reduces the number of changes required when updating navigation libraries in the future.

```javascript
import { useNavigate } from 'react-router-dom';
const navigate = useNavigate();
navigate('/dashboard');
```

## Survey Handling and Conditional Navigation
- Surveys require specific IDs before navigating.
- Conditional checks determine the correct page redirection.
- If a survey is completed, the user is redirected to the report page.
- Otherwise, they are taken to the survey-taking page.

```javascript
const checkSurveyStatus = async (surveyId) => {
  const response = await fetch(`/api/survey/${surveyId}/status`);
  const data = await response.json();
  return data.isCompleted ? '/survey/report' : '/survey/start';
};
```

## Configuration-Based UI Rendering
- UI elements are dynamically enabled or disabled based on configuration settings.
- Module-based permissions determine visible components.
- Organizations can control visibility at a module level by updating configuration settings.

## Module-Based UI Restrictions
- Modules can be hidden or displayed based on organization settings.
- Example: If `soul` is `false`, it will be hidden.
- If the settings array is empty, all modules will be shown.

## Handling Data in Local Storage
- Permissions and user data are stored in local storage for faster access.
- This prevents a brief UI flicker where unauthorized elements appear on refresh.
- Local storage is updated at login and used throughout the session.

## Use of Object Entries, Keys, and Values
- JavaScript functions like `Object.entries()`, `Object.keys()`, and `Object.values()` are heavily used.
- `Object.entries()` is used to iterate over key-value pairs in objects.

```javascript
const permissions = { view: true, edit: false };
Object.entries(permissions).forEach(([key, value]) => {
  console.log(`Permission: ${key}, Allowed: ${value}`);
});
```

## Performance Considerations with `every` and `some`
- `every()` is used to check if all conditions in an array are met.
- `some()` is used to check if at least one condition is met.
- Used for permission validation.
- Example: Checking if a user has all required permissions for an action.

```javascript
const hasAllPermissions = requiredPermissions.every(perm => userPermissions.includes(perm));
const hasSomePermissions = requiredPermissions.some(perm => userPermissions.includes(perm));
```

## Conclusion
This document provides an in-depth look at the key technical components discussed in the Day 1 KT session. By leveraging dynamic configurations, permission-based rendering, and modern React navigation practices, the system ensures efficient and flexible UI management.

# Knowledge Transfer (KT) Documentation - Day 2

## Table of Contents
- [Introduction](#introduction)
- [Dashboard Overview](#dashboard-overview)
- [Permission-Based Rendering](#permission-based-rendering)
- [UI Adjustments and Placement Issues](#ui-adjustments-and-placement-issues)
- [Activity Tracking System](#activity-tracking-system)
- [Survey and Data Handling](#survey-and-data-handling)
- [Query Mechanism](#query-mechanism)
- [GraphQL Playground Usage](#graphql-playground-usage)
- [Super User vs Staff Access](#super-user-vs-staff-access)
- [Team and Organization Management](#team-and-organization-management)
- [Caching and GraphQL Data Handling](#caching-and-graphql-data-handling)
- [Soul Module and Learning Path](#soul-module-and-learning-path)
- [Impact Narrative System](#impact-narrative-system)
- [Aliasing and Query Optimization](#aliasing-and-query-optimization)
- [Conclusion](#conclusion)

---

## Introduction
This document provides a detailed technical and theoretical overview of the topics discussed during the Day 2 Knowledge Transfer (KT) session. The session covered permissions, UI configurations, query handling, GraphQL integration, team management, caching, and advanced navigation mechanisms.

## Dashboard Overview
- The dashboard dynamically displays greeting messages based on the time of the day.
- OKR visibility is based on specific permissions.
- The dashboard does not require explicit permissions for basic access, but some sections appear conditionally.
- If a user has feedback permissions, the feedback button is shown.
- Similar conditions apply to OKR, coaching engagement, and other modules.

## Permission-Based Rendering
- The dashboard itself is accessible to all users.
- Specific elements within the dashboard are displayed based on user permissions.
- Example:
  ```javascript
  if (user.hasPermission('feedback')) {
      showFeedbackButton();
  }
  ```
- Coaching engagement, one-on-one sessions, and other modules are controlled similarly.

## UI Adjustments and Placement Issues
- An icon was initially misplaced, giving a broken UI impression.
- Suggested UI adjustments:
  - Move the icon to the corner.
  - Shift buttons (like "Kudos") for better alignment.

## Activity Tracking System
- The right-side column of the dashboard is reserved for activities.
- Activities include:
  - Meetings
  - Action items
  - Kudos
  - Feedback
  - Diversity surveys (for first-time users)
- First-time users must complete the diversity survey before accessing other activities.

## Survey and Data Handling
- Users must complete surveys like the diversity profile before proceeding.
- Queries are available to check if a user has completed a required survey.
- Example Query:
  ```javascript
  const checkSurveyStatus = async (surveyId) => {
      const response = await fetch(`/api/survey/${surveyId}/status`);
      return response.json();
  };
  ```

## Query Mechanism
- Queries are used to check survey responses and meeting schedules.
- Fetching user permissions is handled through API calls.
- Query example:
  ```graphql
  query getUserPermissions {
    userPermissions {
      view
      edit
    }
  }
  ```

## GraphQL Playground Usage
- The GraphQL Playground provides real-time query execution.
- Features include:
  - Auto-suggestions using `Ctrl + Space`
  - Error messages for missing fields
  - Caching of previously fetched data

## Super User vs Staff Access
- Staff members can access Django Admin.
- Superusers bypass all permission checks.
- It is recommended **not** to test with a superuser account to ensure proper permission validation.

## Team and Organization Management
- Team lists are dynamically fetched based on user roles.
- A team manager can view and manage their teams.
- Example:
  ```javascript
  if (user.role === 'team_manager') {
      fetchUserTeams();
  }
  ```
- Organization data is also dynamically retrieved.

## Caching and GraphQL Data Handling
- GraphQL caches responses to optimize performance.
- Issues arise when the cache holds outdated data.
- Ensuring the presence of IDs in queries prevents UI errors.

## Soul Module and Learning Path
- The "Soul" module is central to the platform.
- Users must complete the learning path before accessing surveys.
- Learning paths include instructional videos and text-based guidance.
- Example:
  ```javascript
  if (!user.hasCompletedLearningPath) {
      showLearningPath();
  }
  ```

## Impact Narrative System
- The Impact Narrative is dynamically generated based on user responses.
- Earlier, users had to manually input their narratives.
- Now, it uses an automated model (`runpods` service) for generation.
- The "Regenerate" button is shown when updates are needed.
- Example flag check:
  ```javascript
  if (user.hasUpdatedValues) {
      showRegenerateButton();
  }
  ```

## Aliasing and Query Optimization
- Aliasing is used to fetch multiple datasets simultaneously.
- Example:
  ```graphql
  query {
    userValues: surveyResponses(surveyId: "values") {
      id
      response
    }
    userStrengths: surveyResponses(surveyId: "strengths") {
      id
      response
    }
  }
  ```
- This avoids multiple API calls and improves efficiency.

## Conclusion
This document captures the key discussions from the Day 2 KT session, focusing on permissions, UI elements, queries, caching, and advanced navigation logic. By leveraging GraphQL, dynamic permission handling, and optimized queries, the system ensures efficient user access and content visibility.

# Knowledge Transfer (KT) Documentation - Day 3

## Table of Contents
- [Introduction](#introduction)
- [Readiness Assessment Overview](#readiness-assessment-overview)
- [Validation and Conditional Checks](#validation-and-conditional-checks)
- [Survey Data Processing](#survey-data-processing)
- [Dynamic Mutation and Query Handling](#dynamic-mutation-and-query-handling)
- [GraphQL Query Optimization](#graphql-query-optimization)
- [OKR (Objectives and Key Results) System](#okr-objectives-and-key-results-system)
- [Task Assignment and Collaboration](#task-assignment-and-collaboration)
- [Milestone Creation and Dependencies](#milestone-creation-and-dependencies)
- [Discard Requests and Approval Workflow](#discard-requests-and-approval-workflow)
- [Correction Deadlines and Editing Restrictions](#correction-deadlines-and-editing-restrictions)
- [Error Handling in API Calls](#error-handling-in-api-calls)
- [Conclusion](#conclusion)

---

## Introduction
This document captures all technical and theoretical discussions from the Day 3 Knowledge Transfer (KT) session. The session focused on the Readiness Assessment process, OKR system, GraphQL optimizations, validation logic, task assignment, and dynamic API mutations.

## Readiness Assessment Overview
- Readiness assessment allows employees and managers to evaluate skills.
- Two types of assessments:
  - Self-assessment (for individuals)
  - Team-assessment (for managers and vertical heads)
- Options available depend on user roles.
- Users select competencies and answer predefined questions.

## Validation and Conditional Checks
- The second question changes dynamically based on the response to the first question.
- Conditional logic ensures valid inputs.
- Example validation rule:
  - If `questionID 688` is between `0-25`, then `questionID 689` must also be between `0-25`.
  - If `questionID 691` is selected, then certain constraints apply.
- Future rule changes only require updating validation parameters.
- The UI uses sliders to capture user responses but processes them as survey data in the backend.

## Survey Data Processing
- Readiness assessment responses are structured as survey data.
- The backend determines the final evaluation score based on survey input.
- Example: The system computes an average value and determines which zone the user falls into.
- Clicking “View” allows users to see the detailed breakdown of scores.

## Dynamic Mutation and Query Handling
- Multiple readiness assessments can be submitted at once.
- Uses **dynamic mutations** instead of looping over individual mutations.
- Example GraphQL mutation with aliasing:
  ```graphql
  mutation {
    create0: createReadiness(input: { skill: "Angular", level: "Intermediate" }) {
      id
    }
    create1: createReadiness(input: { skill: "React", level: "Beginner" }) {
      id
    }
  }
  ```
- This approach reduces network load and prevents unnecessary sequential execution.

## GraphQL Query Optimization
- **Aliasing** is used for querying multiple datasets in a single request.
- Example:
  ```graphql
  query {
    userValues: surveyResponses(surveyId: "values") {
      id
      response
    }
    userStrengths: surveyResponses(surveyId: "strengths") {
      id
      response
    }
  }
  ```
- The system caches responses, but outdated cache entries can sometimes cause UI inconsistencies.
- Fetching the correct organizational data is crucial to avoid frontend crashes.

## OKR (Objectives and Key Results) System
- Users can create and manage OKRs.
- The structure includes:
  - **Objectives**: High-level goals
  - **Key Results (KRs)**: Measurable outcomes under objectives
  - **Milestones**: Stepwise breakdown of key results
- OKRs can be personal or assigned to team members.

## Task Assignment and Collaboration
- Two types of OKR task delegation:
  - **Assignment**: Full responsibility is given to another team member.
  - **Collaboration**: Multiple users work together with percentage-based contributions.
- Assigned tasks require user acceptance before they appear in their dashboard.
- Once assigned, the original owner loses control over the task.
- Collaboration allows task splitting:
  ```javascript
  task.collaborators = [{ user: "Basil", share: 50 }, { user: "Sahil", share: 50 }];
  ```

## Milestone Creation and Dependencies
- Users break down KRs into **Milestones**.
- Constraints:
  - A KR assigned to another user **cannot** have additional milestones.
  - If multiple collaborators exist, they can create milestones.
- Date dependencies:
  - A milestone’s completion date cannot exceed the KR’s deadline.

## Discard Requests and Approval Workflow
- Discarding an OKR requires manager approval.
- Status indicators:
  - **Blue**: Discard requested
  - **Black**: Approved discard
- If rejected, the task remains active.
- Example discard request:
  ```graphql
  mutation {
    discardOKR(input: { id: "12345" }) {
      status
    }
  }
  ```

## Correction Deadlines and Editing Restrictions
- OKRs have a **Correction Deadline** (default: 7 days after creation).
- After the deadline, OKRs cannot be edited or deleted.
- Owners retain control only within the correction window.
- This prevents last-minute changes after evaluations start.

## Error Handling in API Calls
- Errors often occur due to incorrect parameter types in GraphQL queries.
- Example issue: **Expecting ID but received FLOAT**
  - Fix: Ensure type consistency in queries.
- Wrapping API calls in try-catch prevents UI crashes:
  ```javascript
  try {
    const response = await fetch('/api/data');
    const data = await response.json();
  } catch (error) {
    console.error("API Error: ", error);
  }
  ```

## Conclusion
This document provides an extensive breakdown of Day 3 KT topics, covering Readiness Assessments, OKR workflows, validation rules, GraphQL optimizations, and error handling techniques. The knowledge shared in this session ensures structured evaluations, dynamic query processing, and efficient data handling within the system.

# Knowledge Transfer (KT) Documentation - Day 4

## Table of Contents
- [Introduction](#introduction)
- [OKR Page Navigation](#okr-page-navigation)
- [Cascaded and Non-Cascaded Objectives](#cascaded-and-non-cascaded-objectives)
- [Charting and Visualization](#charting-and-visualization)
- [Competency and Skill Mapping](#competency-and-skill-mapping)
- [SVG-Based Tree Structure](#svg-based-tree-structure)
- [GraphQL Data Handling](#graphql-data-handling)
- [Data Structure for Objectives](#data-structure-for-objectives)
- [Pagination in GraphQL](#pagination-in-graphql)
- [Path Class and Data Visualization](#path-class-and-data-visualization)
- [Conclusion](#conclusion)

---

## Introduction
This document provides detailed technical documentation for the Day 4 Knowledge Transfer (KT) session. The discussion covered OKR handling, visualization using charts, SVG-based tree structures, GraphQL queries, and competency mapping within the application.

## OKR Page Navigation
- The OKR page adapts based on the user role.
- Normal users see only **My OKRs**.
- Team managers see both **My OKRs** and **Team OKRs**.
- Vertical heads see **Vertical OKRs**.
- The POC (Point of Contact) sees **Organization OKRs**.

## Cascaded and Non-Cascaded Objectives
- **Non-Cascaded Objectives**: Direct objectives created by the user.
- **Cascaded Objectives**: Objectives created by someone else and assigned or collaborated on.
- Assignment Example:
  - Manager assigns OKR to an employee → Employee sees it as a **cascaded** objective.
  - Collaboration occurs when a user cannot complete an OKR alone.
  
## Charting and Visualization
- **Donut Chart vs. Pie Chart**:
  - A **donut chart** has a hole in the middle.
  - A **pie chart** is a full circle.
- **Chart.js** is used for visualization.
- Older versions are used to maintain compatibility with the project.
- Custom progress bars are implemented for better UI representation.
- Example configurations:
  ```javascript
  const options = {
    responsive: true,
    maintainAspectRatio: false,
  };
  ```

## Competency and Skill Mapping
- **Milestones** may require specific competencies (e.g., React skills for a frontend milestone).
- Competency mapping helps managers track missing skills for employees.
- No direct navigation yet, but potential future feature:
  - Hovering over a competency could link to an **IDP (Individual Development Plan)** page.
  - Example Query:
    ```graphql
    query getCompetency {
      competency(skill: "React Native") {
        id
        description
      }
    }
    ```

## SVG-Based Tree Structure
- **D3.js with React** is used for hierarchical visualization.
- Tree structure shows cascaded OKRs dynamically.
- Objective types are color-coded:
  - **Green** → Objective
  - **Blue** → Key Result
  - **Orange** → Milestone
- **Foreign Object Usage in SVG**:
  - Used to allow rendering HTML elements inside SVG components.
  ```xml
  <foreignObject>
    <div class="custom-label">Objective Name</div>
  </foreignObject>
  ```

## GraphQL Data Handling
- **Aliasing** is used to fetch multiple datasets in one request.
- Pagination is implemented to limit backend load.
- Example query structure:
  ```graphql
  query getOKRs {
    objectives(first: 10) {
      edges {
        node {
          id
          name
        }
      }
    }
  }
  ```
- The frontend dynamically processes and structures this data into a tree.

## Data Structure for Objectives
- JSON-like structure is used for tree rendering.
- Each objective has children that represent assigned KRs.
- Example:
  ```json
  {
    "name": "Frontend Redesign",
    "attributes": {
      "okrType": "Objective"
    },
    "children": [
      {
        "name": "Improve UI Components",
        "attributes": { "okrType": "Key Result" },
        "children": []
      }
    ]
  }
  ```

## Pagination in GraphQL
- Two pagination methods:
  - **Offset Pagination**: Uses `skip` and `limit`.
  - **Cursor Pagination**: Uses `startCursor` and `endCursor`.
- Example Cursor-Based Pagination:
  ```graphql
  query {
    objectives(first: 5, after: "cursor123") {
      edges {
        node {
          id
          name
        }
      }
      pageInfo {
        hasNextPage
        endCursor
      }
    }
  }
  ```

## Path Class and Data Visualization
- **Path Class** determines the styling of connecting lines in the SVG tree.
- Different types of connections are color-coded.
- Example implementation:
  ```javascript
  function getPathClass(target) {
    if (target.attributes.okrType === "Objective") return "objective-path";
    if (target.attributes.okrType === "Key Result") return "key-result-path";
    return "default-path";
  }
  ```
- **Console Logging for Debugging**:
  - Developers console log GraphQL responses to inspect structure.
  - Example:
    ```javascript
    console.log(response.data);
    ```

## Conclusion
This document captures all major aspects discussed during the Day 4 KT session, including OKR structures, competency mapping, GraphQL optimizations, and advanced visualization techniques. The use of D3.js, GraphQL pagination, and hierarchical data structures ensures an efficient and scalable implementation.

# Knowledge Transfer (KT) Documentation - Day 5

## Table of Contents
- [Introduction](#introduction)
- [One-on-One Meeting Feature](#one-on-one-meeting-feature)
- [Scheduling and Recurring Meetings](#scheduling-and-recurring-meetings)
- [RR Rule for Scheduling](#rr-rule-for-scheduling)
- [Meeting Data Handling](#meeting-data-handling)
- [WebSocket Integration](#websocket-integration)
- [Calling and Transcription Process](#calling-and-transcription-process)
- [Error Handling and WebSocket Connection](#error-handling-and-websocket-connection)
- [Conclusion](#conclusion)

---

## Introduction
This document provides a detailed technical breakdown of the features discussed in the Day 5 Knowledge Transfer (KT) session. It covers the implementation of the one-on-one meeting system, scheduling logic, WebSocket handling, transcription processing, and error management.

## One-on-One Meeting Feature
- The one-on-one feature enables users to conduct video or audio meetings.
- There are two ways to initiate a one-on-one:
  1. **Instant Meeting** - Creates a meeting immediately, sending notifications via email.
  2. **Scheduled Meeting** - Allows users to set a date and time.

## Scheduling and Recurring Meetings
- Users can schedule meetings for a specific date and time.
- **Recurring meetings** can be set using various recurrence rules:
  - **Daily** - Meeting occurs every day.
  - **Weekly** - Select specific weekdays for recurrence.
  - **Monthly** - Choose a fixed date or a day within the month.
  - **Custom** - Users can set custom recurrence intervals.
- Example recurrence configuration:
  ```javascript
  const recurrenceRule = {
    frequency: "weekly",
    interval: 1,
    days: ["Monday", "Wednesday", "Friday"],
    until: "2025-03-04T00:00:00Z"
  };
  ```

## RR Rule for Scheduling
- The **RR Rule** is a global standard for handling meeting recurrences (used by Teams, Zoom, etc.).
- The structure follows:
  - **Frequency**: Defines the recurrence type (daily, weekly, etc.).
  - **Interval**: Gap between recurrences (e.g., every 2 weeks).
  - **Days**: Specifies active weekdays for weekly meetings.
  - **Until**: Defines the end date of the recurrence.
- Example RR rule:
  ```json
  {
    "frequency": "weekly",
    "interval": 1,
    "days": ["Monday", "Wednesday", "Friday"],
    "until": "2025-03-04T00:00:00Z"
  }
  ```

## Meeting Data Handling
- The meeting data is processed and stored via API.
- Users can add agendas before the meeting begins.
- Example API call for meeting creation:
  ```graphql
  mutation createMeeting {
    createMeeting(input: {
      title: "KT Call",
      date: "2025-02-25T11:00:00Z",
      duration: 60,
      recurrenceRule: "FREQ=WEEKLY;INTERVAL=1;BYDAY=MO,WE,FR;UNTIL=20250304T000000Z"
    }) {
      id
      status
    }
  }
  ```

## WebSocket Integration
- Meetings use WebSocket connections for real-time synchronization.
- WebSockets handle:
  - Live transcription
  - Meeting state changes
  - Participant notifications
- Connection process:
  ```javascript
  const socket = new WebSocket("wss://meeting-server.com/socket");
  socket.onopen = () => console.log("WebSocket connected");
  socket.onmessage = (event) => processMessage(event.data);
  socket.onerror = (error) => console.error("WebSocket Error: ", error);
  ```

## Calling and Transcription Process
### Calling Process
- Meetings support both video and audio-only calls.
- Peer-to-peer connection is used for direct communication.
- If users are on different networks, a **TURN Server** is required for connection relay.
- Example WebRTC setup:
  ```javascript
  const peerConnection = new RTCPeerConnection(iceServers);
  navigator.mediaDevices.getUserMedia({ video: true, audio: true })
    .then(stream => {
      stream.getTracks().forEach(track => peerConnection.addTrack(track, stream));
    });
  ```

### Transcription Process
1. **User starts recording** - MediaRecorder API is triggered.
2. **Audio is captured in chunks** - Data is processed every few milliseconds.
3. **Recording is converted into binary (BLOB format).**
4. **Data is sent to backend transcription API** (Rust-based API is used).
5. **Backend processes and returns transcribed text via WebSocket.**
6. **Transcription updates dynamically as user speaks.**

- Example MediaRecorder usage:
  ```javascript
  navigator.mediaDevices.getUserMedia({ audio: true }).then(stream => {
    const mediaRecorder = new MediaRecorder(stream);
    mediaRecorder.start();
    mediaRecorder.ondataavailable = event => {
      sendAudioChunk(event.data);
    };
  });
  ```

### WebSocket Integration for Transcription
- WebSockets are used to send real-time transcription updates.
- The frontend listens for messages from the backend and updates the UI.
- Example WebSocket message processing:
  ```javascript
  socket.onmessage = (event) => {
    const transcript = JSON.parse(event.data);
    displayTranscript(transcript.text);
  };
  ```

## Error Handling and WebSocket Connection
- Errors occur when WebSocket connections fail.
- If WebSocket does not connect, buttons for meeting actions are disabled.
- Example error handling:
  ```javascript
  socket.onerror = (error) => {
    console.error("WebSocket Error", error);
    showMessage("Connection failed. Please retry.");
  };
  ```

## Conclusion
This document details the implementation of the one-on-one meeting system, covering scheduling logic, WebSocket integration, and transcription handling. The meeting module ensures efficient scheduling, real-time synchronization, and reliable communication between participants.

# Knowledge Transfer (KT) Documentation - Day 6

## Table of Contents
- [Introduction](#introduction)
- [Call Transcript Handler](#call-transcript-handler)
- [Meeting and OKR Integration](#meeting-and-okr-integration)
- [Transcription Toggle and Call Feature](#transcription-toggle-and-call-feature)
- [Participant Management](#participant-management)
- [Call State Handling](#call-state-handling)
- [Peer-to-Peer (P2P) Connection](#peer-to-peer-p2p-connection)
- [Audio and Video Availability Check](#audio-and-video-availability-check)
- [WebSocket Connection and Error Handling](#websocket-connection-and-error-handling)
- [UI Controls and Call Status Management](#ui-controls-and-call-status-management)
- [Conclusion](#conclusion)

---

## Introduction
This document provides a comprehensive breakdown of the Day 6 Knowledge Transfer (KT) session. The discussion primarily focused on the call transcript handler, meeting and OKR integration, peer-to-peer communication, and WebSocket management for live transcription.

## Call Transcript Handler
- The **Call Transcript Handler** is a reusable component designed for handling transcription across different modules.
- It requires a **letter document**, which contains:
  - **Meeting ID** (if related to a meeting)
  - **OKR ID** (if related to OKRs)
  - **Document Type** (e.g., `Oneonone meeting`, `OKR`)
- This structure allows the transcription feature to be extended to multiple modules with minimal changes.

## Meeting and OKR Integration
- The system allows passing transcription data for different modules:
  - **For meetings:** The `meeting ID` is sent.
  - **For OKRs:** The `OKR ID` is sent.
- The main requirement is the **document ID** and the **document type** to differentiate between various transcription use cases.

## Transcription Toggle and Call Feature
- The transcription system operates independently but can be enabled alongside calls.
- Users can **enable or disable transcription** during a call.
- Example: Like in Microsoft Teams, users can choose to turn on transcription only when necessary.

## Participant Management
- The system currently supports **one-on-one calls**.
- Future scalability for group calls:
  - The **participant list** is structured to allow expansion.
  - UI changes will be required to accommodate multiple participants.

## Call State Handling
- The call state is managed using a dedicated **call state field**.
- UI elements such as the **back button** are disabled when a call is active.
- After ending the call, UI elements revert to their normal state.

## Peer-to-Peer (P2P) Connection
- The system utilizes **Peer-to-Peer (P2P) WebRTC connections**.
- Currently optimized for **one-on-one communication**.
- Future enhancements may require a **TURN server** for handling multiple users across different networks.
- Example WebRTC Setup:
  ```javascript
  const peerConnection = new RTCPeerConnection(iceServers);
  navigator.mediaDevices.getUserMedia({ video: true, audio: true })
    .then(stream => {
      stream.getTracks().forEach(track => peerConnection.addTrack(track, stream));
    });
  ```

## Audio and Video Availability Check
- Before initiating a call, the system checks for **audio and video device availability**.
- If no microphone is detected, the UI disables the microphone toggle option.
- Example media device check:
  ```javascript
  navigator.mediaDevices.enumerateDevices().then(devices => {
    const hasAudio = devices.some(device => device.kind === 'audioinput');
    const hasVideo = devices.some(device => device.kind === 'videoinput');
    updateUI(hasAudio, hasVideo);
  });
  ```

## WebSocket Connection and Error Handling
- **WebSocket is required for real-time transcription.**
- Cookies are set before establishing the WebSocket connection.
- If the WebSocket fails to connect:
  - Icons and buttons for transcription will be disabled.
  - A warning message will be displayed to the user.
- Example WebSocket Handling:
  ```javascript
  const socket = new WebSocket("wss://transcription-server.com/socket");
  socket.onopen = () => console.log("WebSocket connected");
  socket.onmessage = (event) => processTranscription(event.data);
  socket.onerror = (error) => console.error("WebSocket Error: ", error);
  ```

## UI Controls and Call Status Management
- UI elements are dynamically updated based on call status:
  - **When calling:** Disable back button and other navigation options.
  - **When call ends:** Re-enable all UI controls.
  - **When transcription is on:** Display real-time transcribed text.
- Call states include:
  - `Calling`
  - `Ringing`
  - `Connected`
  - `Disconnected`
- Example UI status update:
  ```javascript
  function updateCallUI(status) {
    if (status === 'Calling') disableBackButton();
    else enableBackButton();
  }
  ```

## Conclusion
This document outlines the key technical aspects covered in the Day 6 KT session. It details the **call transcript handler**, **meeting and OKR integration**, **peer-to-peer communication**, **audio/video checks**, **WebSocket connections**, and **UI management** for calls and transcription. The modular architecture ensures easy scalability and future feature extensions.

# Knowledge Transfer (KT) Documentation - Day 7

## Table of Contents
- [Introduction](#introduction)
- [Feedback Module](#feedback-module)
  - [Overview](#overview)
  - [Permissions Handling](#permissions-handling)
  - [Types of Feedback](#types-of-feedback)
  - [Filters and Search](#filters-and-search)
  - [Feedback Submission Flow](#feedback-submission-flow)
  - [UI Components](#ui-components)
- [Coaching Conversation](#coaching-conversation)
  - [Coaching Process](#coaching-process)
  - [Survey Mapping and Alias Filtering](#survey-mapping-and-alias-filtering)
  - [Pagination Strategy](#pagination-strategy)
  - [Conversation Filtering](#conversation-filtering)
- [Survey Handling](#survey-handling)
  - [360 Survey Processing](#360-survey-processing)
  - [Survey UI Workflow](#survey-ui-workflow)
  - [Report Generation](#report-generation)
  - [Terms and Conditions Handling](#terms-and-conditions-handling)
- [Code Flow and API Integration](#code-flow-and-api-integration)
  - [Feedback API Calls](#feedback-api-calls)
  - [Coaching API Calls](#coaching-api-calls)
  - [Survey API Calls](#survey-api-calls)
  - [Real-Time Updates Using Subscriptions](#real-time-updates-using-subscriptions)
- [Conclusion](#conclusion)

---

## Introduction
This document provides a detailed breakdown of the Day 7 KT session. It covers the **Feedback Module**, **Coaching Conversations**, **Survey Handling**, and **Code Flow with API Integration**. The focus is on understanding the theoretical aspects and the technical implementation of these features.

## Feedback Module

### Overview
- The Feedback module allows users to submit, receive, and manage feedback within the system.
- It includes features such as:
  - Motivational and Developmental feedback
  - Kudos integration
  - Filters and search functionality
  - Custom feedback types and validation【77†source】.

### Permissions Handling
- **Four permissions** are required to access the Feedback module:
  1. **Feedback Permission** – Grants access to feedback features.
  2. **Kudos Permission** – Allows users to give motivational kudos.
  3. **OKR Permission** – Enables OKR-based feedback.
  4. **Runboat Permission** – Required for AI-based feedback analysis【77†source】.

### Types of Feedback
1. **Motivational Feedback**
   - Used for encouraging employees based on their performance.
   - Users can add **Kudos** along with the feedback.
   - Example selection:
     ```javascript
     if (feedbackType === 'motivational') {
         enableKudosOption();
     }
     ```

2. **Developmental Feedback**
   - Used to provide constructive suggestions.
   - Kudos cannot be given in this type.
   - Example validation:
     ```javascript
     if (feedbackType === 'developmental') {
         hideKudosOption();
     }
     ```

### Filters and Search
- Users can filter feedback by **time range**:
  - **Past Week**
  - **Past Month**
  - **Past Year**
  - **Custom Date Range**【77†source】.
- Example filter query:
  ```graphql
  query getFilteredFeedback($startDate: String, $endDate: String) {
    feedbackList(filter: { dateRange: { from: $startDate, to: $endDate } }) {
      id
      feedbackText
      date
    }
  }
  ```

### Feedback Submission Flow
- Users can submit feedback via a **modal form**.
- After previewing, feedback can be edited before final submission.
- Example flow:
  ```javascript
  function submitFeedback(data) {
      if (data.isPreviewed) {
          sendToServer(data);
      }
  }
  ```

### UI Components
- **Feedback Tabs**: Received, Submitted, Pending Feedback【77†source】.
- **Input Filters**: Supports only text input currently, dropdowns require separate handling.
- **Feedback Detail Page**: Lists all received feedback with pagination.
- **Pop-up Modals**: Used for kudos and detailed feedback viewing.

## Coaching Conversation

### Coaching Process
- Coaching is a structured interaction between **Coach** and **Coachee**.
- Users select a **Coachee** and associate the coaching session with either:
  - **An OKR (Objective Key Result)**
  - **A Skill (Competency)**【76†source】.

### Survey Mapping and Alias Filtering
- **Coaching Conversations** are stored as surveys in the backend.
- **Alias filtering** is used to retrieve coaching data separately for coaches and coachees.
- Example GraphQL aliasing:
  ```graphql
  query {
    coachSessions: coachingSessions(filter: { role: "coach" }) {
      id
      topic
    }
    coacheeSessions: coachingSessions(filter: { role: "coachee" }) {
      id
      topic
    }
  }
  ```【77†source】.

### Pagination Strategy
- Uses **cursor-based pagination** to improve efficiency.
- Retrieves only the latest **10 conversations** at a time.
- Example query:
  ```graphql
  query getCoachingSessions($cursor: String) {
    coachingSessions(first: 10, after: $cursor) {
      edges {
        node {
          id
          topic
        }
      }
      pageInfo {
        hasNextPage
        endCursor
      }
    }
  }
  ```

### Conversation Filtering
- Filters ensure only the **most recent coaching session** is shown per user.
- Previous sessions are linked under **Next Conversation ID**.

## Survey Handling

### Terms and Conditions Handling
- Surveys require **Terms and Conditions acceptance** before users proceed【79†source】.
- Declining redirects users to the home page.

### Report Generation
- Generates insights and suggestions based on survey responses.

## Code Flow and API Integration

### Real-Time Updates Using Subscriptions
- Feedback updates are received in real-time using GraphQL subscriptions【77†source】.
- Example:
  ```graphql
  subscription feedbackUpdates {
    feedbackReceived {
      id
      feedbackText
    }
  }
  ```

## Conclusion
This document now includes all **minor details** discussed in the session, covering **permissions, UI elements, conversation handling, survey workflow, and real-time updates**.

