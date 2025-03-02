## **Key Discussion Points**

### **1. Dashboard and Navigation Overview**
- **Dashboard Components**: The dashboard contains various components, and navigation is primarily handled through the sidebar.  
- **URL-Based Navigation**: The sidebar navigation is URL-driven. When a user clicks on a menu item, the URL changes, and the corresponding section is highlighted (e.g., green color indicates the selected section).  
- **State Management**: No state is explicitly set for the selected menu item. Instead, the URL determines the active section.  
- **Navigation Code**: The navigation logic is defined in a file called `navigation.js`, where keys and paths are mapped to specific menu items.  

---

### **2. Sidebar Functionality**
- **Dynamic Menu Items**: The sidebar menu items are dynamically displayed based on the user's role (e.g., team managers see additional options like "My Team").  
- **Custom Permissions**: Custom permissions are checked before rendering menu items. If a user doesn’t have the required permissions, certain menu items are hidden.  
- **Local Storage**: User permissions are stored in local storage to prevent flickering of menu items during page refresh.  
- **Module Configuration**: Each module (e.g., HR, OKR) has specific permissions that determine whether it should be displayed in the sidebar.  

---

### **3. Custom Permissions and Role-Based Access**
- **Permission Checks**: Permissions are checked for each module before rendering. For example, HR-related menu items are only visible to users with specific roles (e.g., CU or PUC).  
- **Role-Based Access**: The sidebar dynamically adjusts based on the user's role. For instance, only team managers can see the "My Team" section.  
- **Permission Validation**: A global function (`globalPermissionValidator`) is used to validate permissions across different modules.  

---

### **4. Breadcrumbs and URL Handling**
- **Breadcrumbs**: Breadcrumbs are dynamically generated based on the current URL path. For example, navigating to "Employee Details" will display a breadcrumb like "Home > Employee Details."  
- **URL Matching**: The breadcrumb system matches the URL path with predefined configurations to display the correct hierarchy.  

---

### **5. React Navigation and History Management**
- **React 18 Navigation**: In React 18, the `history` object is replaced with the `navigate` function. This change simplifies navigation and makes it more consistent across the application.  
- **Navigation Function**: A custom navigation function (`navigateRoute`) is created to handle navigation across the application. This function can be easily updated if future React versions introduce changes to the navigation API.  
- **Backward Compatibility**: The codebase still uses `history.push` in some places, but the plan is to migrate to the new `navigate` function for better maintainability.  

---

### **6. Permission Handling and Validation**
- **Permission Fetching**: When a user logs in, their permissions are fetched and stored in the application state. These permissions are used to control access to various modules and features.  
- **Permission Validation**: A global function (`globalPermissionValidator`) is used to validate user permissions. This function checks if the user has the required permissions to access a specific module or feature.  
- **Optional Permissions**: Some permissions are optional (e.g., "run pod" permissions). These are not mandatory for accessing a module but can be used to enable additional features.  

---

### **7. JavaScript Array Methods and Object Handling**
- **Object Methods**: The team discussed JavaScript object methods like `Object.values`, `Object.keys`, and `Object.entries`. These methods are used to extract keys, values, or key-value pairs from objects.  
- **Array Methods**: The `every` and `some` array methods were explained:  
  - **`every`**: Returns `true` if all elements in the array satisfy the given condition.  
  - **`some`**: Returns `true` if at least one element in the array satisfies the given condition.  
- **Permission Validation with Arrays**: The `every` method is used to validate permissions. If all required permissions are present, the user is granted access; otherwise, access is denied.  

---

## **Key Takeaways**
- **URL-Driven Navigation**: The application relies heavily on URL-based navigation, with the sidebar dynamically updating based on the current URL.  
- **Role-Based Access Control**: Custom permissions and role-based access control are implemented to ensure that users only see the menu items and features they are authorized to access.  
- **React Navigation**: The migration from `history` to `navigate` in React 18 simplifies navigation and improves code maintainability.  
- **Permission Validation**: A global permission validation function ensures that users have the necessary permissions to access specific modules or features.  
- **JavaScript Fundamentals**: Understanding JavaScript array and object methods is crucial for handling permissions and navigation logic.
# Technical Documentation for KT Call Transcript

## Overview
This document provides a detailed technical overview of the application discussed during the Knowledge Transfer (KT) call. The application involves a dashboard, user permissions, surveys, and various modules like Soul, Impact Narrative, and Learning Path. The documentation covers the UI components, code flow, and backend logic.

---

## Table of Contents
1. **Dashboard Overview**
2. **User Permissions**
3. **Surveys and Feedback**
4. **Soul Module**
5. **Impact Narrative**
6. **Learning Path**
7. **Code Flow and Best Practices**
8. **Runpod Health Check**
9. **GraphQL Subscriptions**
10. **Conclusion**

---

## 1. Dashboard Overview

### UI Components
- **Custom Messages**: The dashboard displays custom messages like "Good Afternoon" based on the time of day.
- **OKR (Objectives and Key Results)**: The OKR section is displayed based on user permissions. If the user has OKR permission, the section is visible; otherwise, it is hidden.
- **Feedback Button**: The feedback button is displayed only if the user has feedback permission.
- **Coaching Engagement**: Similar to OKR, the coaching engagement section is hidden if the user does not have the required permission.
- **Icons and Layout**: Icons are positioned to avoid distortion. Suggestions were made to move the Kudos button to a corner for better UI experience.

### Dynamic Team Listing
- **Team Manager View**: If the user is a team manager, they can select a team from a dropdown. The dropdown dynamically fetches the list of teams the user manages from the database.
- **Frontend and Backend Integration**: The team list is populated dynamically using an API call. The navigation and team list are managed in the `navigation.js` file.

---

## 2. User Permissions

### Permission Handling
- **Dashboard Access**: The dashboard is accessible to everyone, but certain sections like OKR, feedback, and coaching engagement are displayed based on specific permissions.
- **Permission Checks**: The application checks for permissions before displaying any section. For example, if a user does not have coaching engagement permission, the corresponding section is hidden.
- **Dynamic Permissions**: Permissions are fetched dynamically, and the UI updates accordingly.

### Permission Flow
1. **Fetch Permissions**: The application fetches the user's permissions from the backend.
2. **UI Rendering**: Based on the permissions, the UI renders or hides specific sections.
3. **Feedback and OKR**: If the user has feedback or OKR permissions, the respective buttons and sections are displayed.

---

## 3. Surveys and Feedback

### Survey Completion
- **Diversity Survey**: First-time users are prompted to complete the diversity survey. The application checks if the user has completed the survey using a query.
- **Survey Responses**: The application uses a query to fetch survey responses. If the user has not completed the survey, they are prompted to do so.

### Feedback Mechanism
- **Feedback Button**: The feedback button is displayed only if the user has feedback permission.
- **Feedback Permissions**: The application checks for feedback permissions before allowing the user to submit feedback.

---

## 4. Soul Module

### Overview
- **Soul Hackathon**: The Soul module is designed to help users complete surveys related to values, personality, and skills. The module was initially introduced through in-person hackathons but has since been moved online.
- **Learning Path**: The Learning Path is introduced to guide users through the Soul module. Users can watch videos and complete surveys at their own pace.

### UI Flow
1. **Learning Path**: Users are directed to the Learning Path when they click on the Soul module.
2. **Survey Completion**: Users must complete surveys related to values, personality, and skills before generating an Impact Narrative.
3. **Impact Narrative**: Once all surveys are completed, users can generate their Impact Narrative.

---

## 5. Impact Narrative

### Overview
- **Impact Narrative Generation**: The Impact Narrative is generated based on the user's survey responses. The narrative is updated automatically if the user updates their values, personality, or skills.
- **Regenerate Button**: The regenerate button is displayed if the user updates their survey responses. The button allows the user to regenerate the Impact Narrative.

### Code Flow
1. **Fetch Survey Responses**: The application fetches the latest survey responses.
2. **Check for Updates**: If the user updates their survey responses, the regenerate button is displayed.
3. **Generate Narrative**: The application uses Runpod to generate the Impact Narrative. The Runpod health is checked before generating the narrative.

---

## 6. Learning Path

### Overview
- **Learning Path Introduction**: The Learning Path is designed to guide users through the Soul module. It includes videos and descriptions to help users understand the module.
- **Future Enhancements**: The Learning Path will be extended to other modules in the future.

### UI Components
- **Cards and Banners**: The Learning Path UI includes cards and banners that display information about the module. The content is managed through a config file.
- **Video URLs**: Video URLs are stored in the config file and can be updated dynamically.

---

## 7. Code Flow and Best Practices

### Aliasing in GraphQL
- **Aliasing**: Aliasing is used to fetch data with different names in a single query. This is useful when fetching multiple survey responses in one go.
- **Example**: The application uses aliasing to fetch survey responses for values, personality, and skills in a single query.

### Code Reusability
- **Function Separation**: Functions like Runpod health check are separated to ensure reusability. This allows the same function to be used in multiple places without duplicating code.
- **Clear Intervals**: When using `setInterval` or `setTimeout`, it is important to clear the interval when the component unmounts to avoid memory leaks.

---

## 8. Runpod Health Check

### Overview
- **Runpod Health**: The application checks the health of Runpod before generating the Impact Narrative. If no workers are available, the application displays a message and does not proceed with the generation.
- **Interval Check**: The application checks the Runpod health every 5 minutes to ensure workers are available.

### Code Flow
1. **Fetch Runpod Health**: The application fetches the Runpod health status.
2. **Check Idle Workers**: If no workers are idle, the application displays a message and does not proceed.
3. **Generate Narrative**: If workers are available, the application proceeds with generating the Impact Narrative.

---

## 9. GraphQL Subscriptions

### Overview
- **Subscriptions**: The application uses GraphQL subscriptions to fetch real-time data. Subscriptions are used to check for updates in survey responses and other data.
- **Unsubscribe on Unmount**: When a component unmounts, the application unsubscribes from the subscription to avoid memory leaks.

### Code Flow
1. **Subscribe to Data**: The application subscribes to data using GraphQL subscriptions.
2. **Unsubscribe on Unmount**: When the component unmounts, the application unsubscribes from the subscription.

---

## 10. Conclusion

This documentation provides a comprehensive overview of the application discussed during the KT call. It covers the UI components, user permissions, surveys, and various modules like Soul, Impact Narrative, and Learning Path. The code flow and best practices are also discussed to ensure efficient and reusable code.

---

**End of Document**

# Technical Documentation: KT Call Transcript for Application

## Overview
This document provides a detailed technical overview of the application discussed during the KT (Knowledge Transfer) call. The application involves features related to readiness assessments, OKR (Objectives and Key Results) management, and dynamic mutations. The documentation covers the UI, code flow, and key functionalities discussed during the call.

---

## 1. **Readiness Assessment Module**

### 1.1 **UI Flow**
- **Readiness Level Assessment**: The application allows users to assess their readiness level or that of their team members. The assessment can be done in two ways:
  - **Self-Assessment**: Users can assess their own readiness level.
  - **Team Assessment**: Managers or vertical managers can assess the readiness level of their team members.
  
- **Assessment Page**:
  - Users can select competencies from a list and provide ratings based on their knowledge or skill level.
  - The UI includes a slider to adjust values, which are then validated based on predefined rules.
  - The backend performs validation checks based on the selected values, and the UI updates dynamically.

- **Validation Rules**:
  - The application enforces validation rules based on the selected competency. For example:
    - If the first question's answer is between 0-25, the second question's answer must also be between 0-25.
    - These rules are configurable and can be modified in the backend.

- **Color Coding**:
  - The UI uses color coding to indicate the readiness level (e.g., green, yellow, red) based on the assessment results.
  - The color zones are configurable, and the background color changes based on the user's input.

### 1.2 **Code Flow**
- **Dynamic Validation**:
  - The validation rules are implemented in the backend and are triggered based on the user's input.
  - The frontend dynamically updates the UI based on the validation results.

- **Dynamic Mutations**:
  - The application uses dynamic mutations to handle multiple assessments in a single API call.
  - Instead of looping through each assessment and making individual API calls, the application generates a single query that includes all the assessments.
  - This approach improves performance and reduces network load.

- **Aliasing in Mutations**:
  - The application uses aliasing in GraphQL mutations to handle multiple assessments dynamically.
  - For example, if a user selects three skills, the mutation will generate aliases like `create0`, `create1`, and `create2` for each skill.

---

## 2. **OKR (Objectives and Key Results) Management Module**

### 2.1 **UI Flow**
- **Objective Creation**:
  - Users can create objectives and define key results (KRs) under each objective.
  - Each key result can have milestones that need to be completed to achieve the objective.

- **Assignment and Collaboration**:
  - **Assignment**: A manager can assign a key result to a specific team member. Once assigned, the responsibility for completing the key result lies with the assigned person.
  - **Collaboration**: Users can collaborate with others on a key result. Collaborators share the responsibility, and the workload can be divided (e.g., 50-50 or 90-10).

- **Discard Request**:
  - If a key result is no longer needed, users can request to discard it.
  - The request must be approved by the manager. Once approved, the key result is marked as discarded and cannot be edited further.

- **Correction Deadline**:
  - Users can edit or delete objectives and key results only within a correction deadline (e.g., 7 days after creation).
  - After the deadline, the objective or key result becomes read-only.

### 2.2 **Code Flow**
- **Objective and Key Result Creation**:
  - The application uses GraphQL mutations to create objectives and key results.
  - The frontend sends a mutation request to the backend, which then stores the data in the database.

- **Dynamic Collaboration**:
  - The application allows users to dynamically add collaborators to a key result.
  - The frontend updates the UI to reflect the collaboration status, and the backend handles the data accordingly.

- **Discard Request Handling**:
  - When a user requests to discard a key result, the application sends a mutation request to the backend.
  - The backend updates the status of the key result and notifies the manager for approval.

---

## 3. **Dynamic Mutations**

### 3.1 **Overview**
- Dynamic mutations are used to handle multiple API calls in a single request. This is particularly useful when dealing with assessments or key results that involve multiple inputs.

### 3.2 **Code Flow**
- **Query Generation**:
  - The frontend dynamically generates a GraphQL query based on the number of inputs (e.g., skills, assessments).
  - The query includes aliases for each input, such as `create0`, `create1`, etc.

- **Mutation Execution**:
  - The generated query is sent to the backend in a single API call.
  - The backend processes the query and returns the results for each input.

- **Error Handling**:
  - If any of the mutations fail, the backend returns an error for the specific input while still processing the successful ones.
  - The frontend can then display the error to the user without affecting the rest of the data.

---

## 4. **UI Components and Features**

### 4.1 **Slider for Input**
- The application uses a slider UI component to allow users to input values for assessments.
- The slider dynamically updates the UI based on the user's input and enforces validation rules.

### 4.2 **Color Zones**
- The UI uses color zones to indicate the status of assessments or key results.
- The colors are configurable and can be changed in the backend.

### 4.3 **Tab Switching**
- The application uses tab switching to navigate between different sections (e.g., self-assessment, team assessment).
- The tab switching logic is implemented using a dynamic object that maps each tab to its corresponding container.

---

## 5. **Error Handling and Debugging**

### 5.1 **Error Handling in Mutations**
- The application handles errors in dynamic mutations by returning specific error messages for each input.
- This allows the frontend to display detailed error messages to the user.

### 5.2 **Debugging Tips**
- **API Calls**: Ensure that all API calls are wrapped in try-catch blocks to handle errors gracefully.
- **Dynamic Mutations**: When using dynamic mutations, ensure that the query is generated correctly and that the backend can handle the input format.

---

## 6. **Future Enhancements**
- **Dynamic Rule Configuration**: Allow users to configure validation rules directly from the UI.
- **Performance Optimization**: Further optimize the performance of dynamic mutations for large datasets.
- **UI Improvements**: Consider using card-based layouts for OKR management to improve usability.

---

## Conclusion
This documentation provides a comprehensive overview of the application's features, UI components, and code flow as discussed during the KT call. The application leverages dynamic mutations, validation rules, and color-coded UI elements to provide a seamless user experience. Future enhancements can further improve the application's performance and usability.
# Technical Documentation: OKR and Competency Integration

## Overview

This document provides a detailed explanation of the OKR (Objectives and Key Results) and Competency integration within the application. The focus is on the UI components, code flow, and the potential enhancement of linking competencies to Individual Development Plans (IDP).

---

## 1. **OKR and Milestones**

### 1.1 **Milestone Overview**
- **Milestone** is the final level of an objective.
- It represents a specific task or deliverable that needs to be completed to achieve the objective.
- Milestones can be associated with specific **competencies** (skills) required to complete them.

### 1.2 **UI Representation**
- Milestones are displayed in the UI with associated competencies.
- Competencies are shown as tags or labels next to the milestone.
- Example: If a milestone requires React Native skills, the competency "React Native" will be displayed next to the milestone.

### 1.3 **Code Flow**
- **Data Structure**: Each milestone object contains a list of competencies.
- **Rendering**: The UI fetches the milestone data and displays the associated competencies.
- **Example**:
  ```javascript
  const milestone = {
    id: 1,
    name: "Complete React Native Task",
    competencies: ["React Native", "JavaScript"]
  };
  ```

---

## 2. **Competency Integration**

### 2.1 **Competency Overview**
- **Competency** refers to the skills required to complete a milestone.
- Competencies are displayed in the UI but do not have any navigation or detailed view associated with them.
- They are purely informational and help managers and users understand the skills needed to complete a task.

### 2.2 **UI Representation**
- Competencies are displayed as tags or labels next to the milestone.
- Example: If a milestone requires React Native, the competency "React Native" will be shown as a tag.

### 2.3 **Code Flow**
- **Data Structure**: Competencies are stored as an array within the milestone object.
- **Rendering**: The UI iterates over the competencies array and renders each competency as a tag.
- **Example**:
  ```javascript
  const milestone = {
    id: 1,
    name: "Complete React Native Task",
    competencies: ["React Native", "JavaScript"]
  };

  // Rendering Competencies
  milestone.competencies.map((competency, index) => (
    <span key={index} className="competency-tag">{competency}</span>
  ));
  ```

---

## 3. **Potential Enhancement: Linking Competencies to IDP**

### 3.1 **Proposed Feature**
- **Objective**: To allow users to directly link competencies required for a milestone to their Individual Development Plan (IDP).
- **Feature Description**: When a user hovers over a competency, a dropdown option "Add to IDP" will appear. Clicking on this option will navigate the user to the IDP creation page with the competency pre-filled.

### 3.2 **UI Flow**
1. **Hover Over Competency**: When a user hovers over a competency tag, a dropdown with the option "Add to IDP" appears.
2. **Click "Add to IDP"**: The user is redirected to the IDP creation page.
3. **Pre-filled Competency**: The competency ID is passed as a URL parameter, and the corresponding skill is auto-filled in the IDP form.

### 3.3 **Code Flow**
- **Hover Interaction**: The UI listens for hover events on competency tags and displays the "Add to IDP" option.
- **Navigation**: On clicking "Add to IDP", the user is redirected to the IDP creation page with the competency ID as a URL parameter.
- **Example**:
  ```javascript
  const handleAddToIDP = (competencyId) => {
    window.location.href = `/idp/create?skill=${competencyId}`;
  };

  // Hover and Click Logic
  <div onMouseEnter={() => setShowDropdown(true)} onMouseLeave={() => setShowDropdown(false)}>
    <span className="competency-tag">{competency}</span>
    {showDropdown && (
      <div className="dropdown">
        <button onClick={() => handleAddToIDP(competency.id)}>Add to IDP</button>
      </div>
    )}
  </div>
  ```

### 3.4 **IDP Page Integration**
- **URL Parameter**: The competency ID is passed as a query parameter.
- **Auto-fill**: The IDP form fetches the competency details based on the ID and auto-fills the skill field.
- **Example**:
  ```javascript
  const urlParams = new URLSearchParams(window.location.search);
  const skillId = urlParams.get('skill');

  // Fetch Competency Details
  const competency = fetchCompetencyDetails(skillId);

  // Auto-fill IDP Form
  <input type="text" value={competency.name} readOnly />
  ```

---

## 4. **Future Considerations**

### 4.1 **Complexity Management**
- **Challenge**: Adding this feature will increase the complexity of the application due to the additional connections between OKR, competencies, and IDP.
- **Solution**: Proper planning and modular code design will help manage this complexity. The feature should be implemented in phases, starting with basic functionality and gradually adding more advanced features.

### 4.2 **User Experience**
- **Challenge**: Users may find it overwhelming if too many options are presented at once.
- **Solution**: The UI should be designed to be intuitive, with clear instructions and tooltips to guide users through the process.

### 4.3 **Client Feedback**
- **Next Steps**: Before implementing this feature, it is recommended to discuss it with the client (Harshad) to ensure it aligns with their vision and requirements.

---

## 5. **Conclusion**

This documentation outlines the current implementation of OKR and competency integration within the application and proposes a potential enhancement to link competencies to IDP. The proposed feature aims to improve the user experience by providing a seamless way to add required skills to their development plans. Further discussions with the client and careful planning will be essential to successfully implement this feature.

--- 

This documentation provides a comprehensive overview of the current system and a proposed enhancement, ensuring that all technical details are well-documented for future reference.
# Technical Documentation: KT Call Application

## Overview
This document provides a detailed technical overview of the KT (Knowledge Transfer) Call Application. The application facilitates one-on-one video calls, scheduling meetings, and transcription of audio calls. The application supports instant and scheduled meetings, series meetings, and integrates with WebSocket for real-time communication. The transcription feature converts audio to text using a backend API.

---

## Table of Contents
1. **Application Features**
2. **User Interface (UI)**
3. **Meeting Scheduling**
4. **Series Meetings**
5. **WebSocket Integration**
6. **Transcription Flow**
7. **Code Flow**
8. **Error Handling**
9. **Future Enhancements**

---

## 1. Application Features
- **Instant Meetings**: Users can initiate one-on-one video calls instantly without scheduling.
- **Scheduled Meetings**: Users can schedule meetings for a future date and time.
- **Series Meetings**: Users can create recurring meetings (daily, weekly, monthly).
- **Transcription**: Audio from the call is transcribed in real-time.
- **Agenda and Action Items**: Users can add agendas and action items for meetings.
- **Feedback**: Users can provide feedback during or after the meeting.

---

## 2. User Interface (UI)
The UI of the application is designed to be intuitive and user-friendly. Below are the key components:

### 2.1. Meeting Scheduling Page
- **Title Field**: Users can enter a title for the meeting.
- **Date and Time Selection**: Users can select the date and time for the meeting.
- **Duration**: Users can set the duration of the meeting (default is 1 hour).
- **Series Meeting Option**: Users can create recurring meetings with options for daily, weekly, or monthly recurrence.
- **Agenda Field**: Users can add an agenda for the meeting.
- **Action Items**: Users can add action items during the meeting.

### 2.2. Meeting Page
- **Start Meeting Button**: Initiates the meeting.
- **Agenda Display**: Displays the agenda for the meeting.
- **Transcription Panel**: Displays real-time transcription of the audio.
- **Action Items Panel**: Allows users to add and view action items.
- **Feedback Button**: Allows users to provide feedback during or after the meeting.

### 2.3. Transcription UI
- **Transcription Status**: Displays whether transcription is active or inactive.
- **Transcription Text**: Displays the transcribed text in real-time.
- **Recording Indicator**: A red icon in the browser tab indicates that recording is active.

---

## 3. Meeting Scheduling
### 3.1. Instant Meetings
- Users can initiate an instant meeting by clicking the "Instant Meeting" button.
- An email notification is sent to the participant with a link to join the meeting.

### 3.2. Scheduled Meetings
- Users can schedule a meeting by selecting a date, time, and duration.
- The meeting is added to the user's calendar, and reminders are sent via email.

### 3.3. Series Meetings
- Users can create recurring meetings with options for daily, weekly, or monthly recurrence.
- Users can specify the end date for the series.
- Users can skip specific days (e.g., skip Tuesdays).

---

## 4. Series Meetings
### 4.1. Recurrence Rules
- **Daily**: The meeting repeats every day.
- **Weekly**: The meeting repeats on selected weekdays (e.g., Monday, Wednesday, Friday).
- **Monthly**: The meeting repeats on a specific date each month (e.g., the 1st of every month).

### 4.2. End Date
- Users can specify an end date for the series.
- The series will automatically stop after the end date.

### 4.3. Editing Series Meetings
- Users can edit individual occurrences of a series meeting without affecting the rest of the series.
- Editing the series itself will affect all future occurrences.

---

## 5. WebSocket Integration
The application uses WebSocket for real-time communication between users and the backend.

### 5.1. WebSocket Connection
- The WebSocket connection is established when the meeting page is loaded.
- The connection is used to send and receive real-time data, such as transcription text and meeting status.

### 5.2. WebSocket Events
- **onopen**: Triggered when the WebSocket connection is successfully established.
- **onmessage**: Triggered when a message is received from the server.
- **onclose**: Triggered when the WebSocket connection is closed.
- **onerror**: Triggered when an error occurs in the WebSocket connection.

### 5.3. WebSocket Messages
- **Transcription Initiated**: Sent when transcription starts.
- **Transcription Confirmed**: Sent when the other user confirms the transcription.
- **Transcription Terminated**: Sent when transcription stops.

---

## 6. Transcription Flow
### 6.1. Recording Audio
- The application uses the browser's `Navigator.mediaDevices.getUserMedia` API to access the user's microphone.
- The audio is recorded in chunks and sent to the backend for transcription.

### 6.2. Transcription API
- The backend API processes the audio and returns the transcribed text.
- The transcription is displayed in real-time on the UI.

### 6.3. Handling Silence
- The application uses an audio analyzer to detect when the user is speaking.
- If the user stops speaking for a certain period, the recording stops, and the audio is sent for transcription.

### 6.4. Audio Chunking
- The audio is recorded in chunks and converted to a BLOB (Binary Large Object).
- The BLOB is sent to the backend as form data.

### 6.5. Transcription Display
- The transcribed text is displayed in the UI in real-time.
- The text is grouped by chunks to ensure continuity.

---

## 7. Code Flow
### 7.1. Initialization
- The WebSocket connection is initialized when the meeting page is loaded.
- The user's microphone is accessed using `Navigator.mediaDevices.getUserMedia`.

### 7.2. Recording Audio
- The audio is recorded using the `MediaRecorder` API.
- The audio is analyzed using the `AudioContext` API to detect when the user is speaking.

### 7.3. Sending Audio to Backend
- The recorded audio is converted to a BLOB and sent to the backend as form data.
- The backend processes the audio and returns the transcribed text.

### 7.4. Displaying Transcription
- The transcribed text is received via WebSocket and displayed in the UI.
- The text is grouped by chunks to ensure continuity.

### 7.5. Stopping Recording
- The recording stops when the user stops speaking or manually stops the recording.
- The audio tracks are stopped to ensure the microphone is no longer accessed.

---

## 8. Error Handling
### 8.1. WebSocket Errors
- If the WebSocket connection fails, an error message is displayed to the user.
- The application attempts to reconnect to the WebSocket.

### 8.2. Microphone Access Errors
- If the user denies access to the microphone, an error message is displayed.
- The user is prompted to allow microphone access.

### 8.3. Transcription Errors
- If the transcription API fails, an error message is displayed.
- The application retries sending the audio to the backend.

---

## 9. Future Enhancements
- **Video Transcription**: Add support for video transcription.
- **Multi-language Support**: Add support for multiple languages in transcription.
- **Improved Noise Cancellation**: Enhance noise cancellation for better audio quality.
- **Integration with Calendar**: Integrate with external calendars (e.g., Google Calendar, Outlook).

---

## Conclusion
The KT Call Application is a robust solution for one-on-one video calls, meeting scheduling, and real-time transcription. The application leverages WebSocket for real-time communication and provides a seamless user experience. Future enhancements will further improve the application's functionality and usability.

--- 

This documentation provides a comprehensive overview of the KT Call Application, covering all aspects from UI to code flow and error handling.

# Technical Documentation: Video Call and Transcription Feature

## Overview
This documentation provides a detailed explanation of the video call and transcription feature implemented in the application. The feature allows users to initiate video calls, manage call states, handle transcription, and manage media devices (audio and video). The system is designed to be modular, allowing it to be reused across different modules with minimal changes.

## Key Components
1. **Call Transcript Handler**: Manages the transcription of calls.
2. **Call State Management**: Handles the state of the call (e.g., calling, ringing, connected).
3. **Media Device Management**: Manages audio and video devices.
4. **Peer-to-Peer Connection**: Handles the connection between users using WebRTC.
5. **WebSocket Communication**: Manages real-time communication between users.
6. **UI Components**: Handles the user interface for call initiation, call acceptance, and call management.

---

## Detailed Functionality

### 1. **Call Transcript Handler**
The call transcript handler is responsible for managing the transcription of calls. It is designed to be reusable across different modules (e.g., meetings, OKRs). The handler requires the following props:
- **Document ID**: Unique identifier for the call (e.g., meeting ID, OKR ID).
- **Document Type**: Specifies the type of document (e.g., one-on-one meeting, OKR).
- **Participants**: List of members in the call.

#### Key Features:
- **Transcription Enable/Disable**: The transcription can be enabled or disabled during the call.
- **Participant Management**: The system currently supports two participants but is designed to handle multiple participants in the future.
- **Call State Management**: The call state (e.g., calling, ringing, connected) is managed to ensure proper UI updates (e.g., disabling the back button during a call).

---

### 2. **Call State Management**
The call state is managed to ensure proper UI updates and functionality during different stages of the call. The following states are handled:
- **Calling**: The call is being initiated.
- **Ringing**: The call is ringing on the recipient's side.
- **Connected**: The call is connected.
- **Disconnected**: The call has ended.

#### Key Features:
- **Call State Timeout**: If the call is not answered within 30 seconds, it is automatically canceled.
- **Call Reconnection**: If the network is lost, the system attempts to reconnect the call within a specified time frame (e.g., 30 seconds).

---

### 3. **Media Device Management**
The system checks for the availability of audio and video devices before initiating a call. This ensures that the call can proceed without issues.

#### Key Features:
- **Media Availability Check**: The system checks if the user's device has a microphone and camera.
- **Device Enumeration**: The system enumerates all available audio and video devices.
- **Device Status Management**: The system manages the status of audio and video devices (e.g., enabling/disabling the microphone or camera during the call).

#### Code Example:
```javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true })
  .then(stream => {
    // Handle the stream
  })
  .catch(error => {
    // Handle errors (e.g., no microphone or camera available)
  });
```

---

### 4. **Peer-to-Peer Connection**
The system uses WebRTC for peer-to-peer communication. The connection is established using the `simple-peer` library.

#### Key Features:
- **Initiator and Receiver**: The user who initiates the call is the initiator, and the user who receives the call is the receiver.
- **Signal Data Exchange**: Signal data (e.g., offer, answer) is exchanged between users to establish the connection.
- **Stream Management**: The system manages the local and remote video streams.

#### Code Example:
```javascript
const peer = new SimplePeer({
  initiator: true,
  stream: localStream,
  config: {
    iceServers: [
      { urls: 'stun:stun.l.google.com:19302' },
      { urls: 'turn:turn.example.com', username: 'user', credential: 'pass' }
    ]
  }
});

peer.on('signal', data => {
  // Send signal data to the other user via WebSocket
});

peer.on('stream', remoteStream => {
  // Handle the remote stream
});
```

---

### 5. **WebSocket Communication**
WebSocket is used for real-time communication between users. The system sends and receives signaling messages (e.g., offer, answer, ice candidates) via WebSocket.

#### Key Features:
- **Signal Data Exchange**: The system sends and receives signal data (e.g., offer, answer) to establish the peer-to-peer connection.
- **Call State Updates**: The system sends call state updates (e.g., calling, ringing, connected) via WebSocket.
- **Reconnection Handling**: If the WebSocket connection is lost, the system attempts to reconnect.

#### Code Example:
```javascript
const socket = new WebSocket('ws://example.com/socket');

socket.onmessage = event => {
  const data = JSON.parse(event.data);
  if (data.type === 'offer') {
    // Handle offer signal
  } else if (data.type === 'answer') {
    // Handle answer signal
  }
};
```

---

### 6. **UI Components**
The UI components handle the user interface for call initiation, call acceptance, and call management.

#### Key Features:
- **Call Initiation UI**: The UI for initiating a call includes a call button and a popup for confirmation.
- **Call Acceptance UI**: The UI for accepting a call includes buttons for accepting or rejecting the call.
- **Call Management UI**: The UI for managing the call includes buttons for muting/unmuting audio, enabling/disabling video, and ending the call.

#### UI Flow:
1. **Call Initiation**:
   - The user clicks the call button.
   - A popup appears asking for confirmation to initiate the call.
   - If the user confirms, the call is initiated, and the call state is set to "calling."

2. **Call Acceptance**:
   - The recipient sees an incoming call UI with buttons to accept or reject the call.
   - If the recipient accepts the call, the call state is set to "connected."

3. **Call Management**:
   - During the call, the user can mute/unmute audio, enable/disable video, and end the call.
   - The UI updates to reflect the current call state (e.g., muted audio, disabled video).

---

## Code Flow

### 1. **Call Initiation**
- The user clicks the call button.
- The system checks for media device availability.
- The system initiates a peer-to-peer connection and sends an offer signal via WebSocket.
- The call state is set to "calling."

### 2. **Call Acceptance**
- The recipient receives the offer signal via WebSocket.
- The recipient accepts the call and sends an answer signal via WebSocket.
- The call state is set to "connected."

### 3. **Call Management**
- During the call, the user can mute/unmute audio, enable/disable video, and end the call.
- The system updates the UI to reflect the current call state.

### 4. **Call Termination**
- The user ends the call by clicking the end call button.
- The system sends a call termination signal via WebSocket.
- The call state is set to "disconnected," and the UI is reset.

---

## Error Handling
- **Media Device Errors**: If the user's device does not have a microphone or camera, the system disables the corresponding UI elements.
- **WebSocket Errors**: If the WebSocket connection is lost, the system attempts to reconnect.
- **Call Timeout**: If the call is not answered within 30 seconds, it is automatically canceled.

---

## Reconnection Handling
- If the network is lost during a call, the system attempts to reconnect within 30 seconds.
- If the network is restored within the timeout period, the call is reconnected automatically.
- If the network is not restored within the timeout period, the call is terminated.

---

## Transcription Handling
- The transcription feature runs in the background during the call.
- If the user mutes the audio, the transcription is also muted.
- The transcription is saved and can be accessed after the call ends.

---

## Conclusion
This documentation provides a comprehensive overview of the video call and transcription feature. The system is designed to be modular, reusable, and robust, with proper error handling and reconnection mechanisms. The UI is intuitive and provides a seamless user experience.

# Technical Documentation: Video Call and Transcription Feature

## Overview
This documentation provides a detailed explanation of the video call and transcription feature implemented in the application. The feature allows users to initiate video calls, manage call states, handle transcription, and manage media devices (audio and video). The system is designed to be modular, allowing it to be reused across different modules with minimal changes.

## Key Components
1. **Call Transcript Handler**: Manages the transcription of calls.
2. **Call State Management**: Handles the state of the call (e.g., calling, ringing, connected).
3. **Media Device Management**: Manages audio and video devices.
4. **Peer-to-Peer Connection**: Handles the connection between users using WebRTC.
5. **WebSocket Communication**: Manages real-time communication between users.
6. **UI Components**: Handles the user interface for call initiation, call acceptance, and call management.

---

## Detailed Functionality

### 1. **Call Transcript Handler**
The call transcript handler is responsible for managing the transcription of calls. It is designed to be reusable across different modules (e.g., meetings, OKRs). The handler requires the following props:
- **Document ID**: Unique identifier for the call (e.g., meeting ID, OKR ID).
- **Document Type**: Specifies the type of document (e.g., one-on-one meeting, OKR).
- **Participants**: List of members in the call.

#### Key Features:
- **Transcription Enable/Disable**: The transcription can be enabled or disabled during the call.
- **Participant Management**: The system currently supports two participants but is designed to handle multiple participants in the future.
- **Call State Management**: The call state (e.g., calling, ringing, connected) is managed to ensure proper UI updates (e.g., disabling the back button during a call).

---

### 2. **Call State Management**
The call state is managed to ensure proper UI updates and functionality during different stages of the call. The following states are handled:
- **Calling**: The call is being initiated.
- **Ringing**: The call is ringing on the recipient's side.
- **Connected**: The call is connected.
- **Disconnected**: The call has ended.

#### Key Features:
- **Call State Timeout**: If the call is not answered within 30 seconds, it is automatically canceled.
- **Call Reconnection**: If the network is lost, the system attempts to reconnect the call within a specified time frame (e.g., 30 seconds).

---

### 3. **Media Device Management**
The system checks for the availability of audio and video devices before initiating a call. This ensures that the call can proceed without issues.

#### Key Features:
- **Media Availability Check**: The system checks if the user's device has a microphone and camera.
- **Device Enumeration**: The system enumerates all available audio and video devices.
- **Device Status Management**: The system manages the status of audio and video devices (e.g., enabling/disabling the microphone or camera during the call).

#### Code Example:
```javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true })
  .then(stream => {
    // Handle the stream
  })
  .catch(error => {
    // Handle errors (e.g., no microphone or camera available)
  });
```

---

### 4. **Peer-to-Peer Connection**
The system uses WebRTC for peer-to-peer communication. The connection is established using the `simple-peer` library.

#### Key Features:
- **Initiator and Receiver**: The user who initiates the call is the initiator, and the user who receives the call is the receiver.
- **Signal Data Exchange**: Signal data (e.g., offer, answer) is exchanged between users to establish the connection.
- **Stream Management**: The system manages the local and remote video streams.

#### Code Example:
```javascript
const peer = new SimplePeer({
  initiator: true,
  stream: localStream,
  config: {
    iceServers: [
      { urls: 'stun:stun.l.google.com:19302' },
      { urls: 'turn:turn.example.com', username: 'user', credential: 'pass' }
    ]
  }
});

peer.on('signal', data => {
  // Send signal data to the other user via WebSocket
});

peer.on('stream', remoteStream => {
  // Handle the remote stream
});
```

---

### 5. **WebSocket Communication**
WebSocket is used for real-time communication between users. The system sends and receives signaling messages (e.g., offer, answer, ice candidates) via WebSocket.

#### Key Features:
- **Signal Data Exchange**: The system sends and receives signal data (e.g., offer, answer) to establish the peer-to-peer connection.
- **Call State Updates**: The system sends call state updates (e.g., calling, ringing, connected) via WebSocket.
- **Reconnection Handling**: If the WebSocket connection is lost, the system attempts to reconnect.

#### Code Example:
```javascript
const socket = new WebSocket('ws://example.com/socket');

socket.onmessage = event => {
  const data = JSON.parse(event.data);
  if (data.type === 'offer') {
    // Handle offer signal
  } else if (data.type === 'answer') {
    // Handle answer signal
  }
};
```

---

### 6. **UI Components**
The UI components handle the user interface for call initiation, call acceptance, and call management.

#### Key Features:
- **Call Initiation UI**: The UI for initiating a call includes a call button and a popup for confirmation.
- **Call Acceptance UI**: The UI for accepting a call includes buttons for accepting or rejecting the call.
- **Call Management UI**: The UI for managing the call includes buttons for muting/unmuting audio, enabling/disabling video, and ending the call.

#### UI Flow:
1. **Call Initiation**:
   - The user clicks the call button.
   - A popup appears asking for confirmation to initiate the call.
   - If the user confirms, the call is initiated, and the call state is set to "calling."

2. **Call Acceptance**:
   - The recipient sees an incoming call UI with buttons to accept or reject the call.
   - If the recipient accepts the call, the call state is set to "connected."

3. **Call Management**:
   - During the call, the user can mute/unmute audio, enable/disable video, and end the call.
   - The UI updates to reflect the current call state (e.g., muted audio, disabled video).

---

## Code Flow

### 1. **Call Initiation**
- The user clicks the call button.
- The system checks for media device availability.
- The system initiates a peer-to-peer connection and sends an offer signal via WebSocket.
- The call state is set to "calling."

### 2. **Call Acceptance**
- The recipient receives the offer signal via WebSocket.
- The recipient accepts the call and sends an answer signal via WebSocket.
- The call state is set to "connected."

### 3. **Call Management**
- During the call, the user can mute/unmute audio, enable/disable video, and end the call.
- The system updates the UI to reflect the current call state.

### 4. **Call Termination**
- The user ends the call by clicking the end call button.
- The system sends a call termination signal via WebSocket.
- The call state is set to "disconnected," and the UI is reset.

---

## Error Handling
- **Media Device Errors**: If the user's device does not have a microphone or camera, the system disables the corresponding UI elements.
- **WebSocket Errors**: If the WebSocket connection is lost, the system attempts to reconnect.
- **Call Timeout**: If the call is not answered within 30 seconds, it is automatically canceled.

---

## Reconnection Handling
- If the network is lost during a call, the system attempts to reconnect within 30 seconds.
- If the network is restored within the timeout period, the call is reconnected automatically.
- If the network is not restored within the timeout period, the call is terminated.

---

## Transcription Handling
- The transcription feature runs in the background during the call.
- If the user mutes the audio, the transcription is also muted.
- The transcription is saved and can be accessed after the call ends.

---

## Conclusion
This documentation provides a comprehensive overview of the video call and transcription feature. The system is designed to be modular, reusable, and robust, with proper error handling and reconnection mechanisms. The UI is intuitive and provides a seamless user experience.
