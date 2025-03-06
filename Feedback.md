## Feedback
+ **KT Provided By**: Amal Santhosh, Basil Eldhose
+ **KT Received By**: Dnyaneshwar Kolhe, Sahil Tamang
+ **Documentation Created By**: Dnyaneshwar Kolhe
### Overview
- The Feedback module allows users to submit, receive, and manage feedback within the system.
- It includes features such as:
  - Motivational and Developmental feedback
  - Kudos integration
  - Filters and search functionality
  - Custom feedback types and validation
### User Guide
- The feedback page has following component
- **Give feedback button**: This will open form to give feedback. Feedback form includes the following fields
  - There are two types of feedback you can give
    - **Motivational/Recognition**: This feedback is given when we want to praise someone for their work or learnings, etc.
    - **Developmental/Constructive**: If we found that someone is lacking in their skills/ work, or they need to work on some part, then in that case we can give this feedback.
  - Then we need to select Recipient, who is going to recieve that feedback
  - Once we select feedback, there is a button called OKR. If you have to give feedback related to any particular OKR then you can click that button, and you will get an option to select the OKR added by the corresponding person.
  - If you are giving Motivational feedback, you can see an option to give Kudos, this option is hidden in case of Developmental feedback.
  - Then we have claps module using which you can give feedback step by step
    - C - Create Safety by stating how the feedback will help the receiver.
    - L - Lay out context by referring to a specific situation, so the feedback is not generalized.
    - A - Articulate behavioral evidence by describing actions/speech objectively and without personal opinions.
    - P - Probe for possible alternatives that the receiver can try to act on the feedback.
    - S - Support for next steps and commitments by offering help, advice and by being an accountability partner.
  - P is a suggestion for the receiver about things he can try for improvement, so it can give in case of developmental feedback only
  - There is also one more toggle called detailed, if you enable it, you can see separate inputs instead of a single description box.
  - When you review the details for all modules in claps, you can preview and submit feedback or you can go back and change the feedback.
- **Demo button**: Upon click, this button will show video about how to give feedback
- **Tool button**: This contains additional information about giving feedback
- **Tablist for Submitted, Received and Pending feedback**: these are the 3 tabs under which we can see all feedback that we have given, received and which we should have given but still pending
- In received feedback, we can see the feedback as cards, we can click on the cards to see details
- In Submitted feedback, cards and working all are the same, we just get the extra button to edit or delete the feedback. 
  - Only the claps module description is editable, and we can add kudos in case of developmental feedback
- In the submitted and received tabs, you can filter the feedbacks using Past Week, Past Month, Past Year, Custom, Clear
- Pending feedback tab is not for all, it's only for managers. 
  - If you haven't given feedback to the team members in the last 30 days, here you can see the feedback is pending, and last feedback given date. 
  - If you click the card, a Popup will open to give feedback with the recipient already selected.
  - If you are a manager, but you have given all the feedback, there is no pending feedback, then this tab won't be listed(Not visible)
- We can give feedback from three places, Dashboard, one-on-one and feedback module.
#### Casper
- There is a purple icon at the bottom right corner, it's an AI chatbot named Casper which is currently working only for feedback and you need permissions otherwise you can't see the icon there.
- You can ask your question about feedback to it, you can either type or speak, it has a speech-to-text feature as well. 
### Technical Breakdown
- NewViewFeedbackContainer.jsx, this is the entry file, the feedback and rest of the things are at the same location
- We have AiTipForPreview function in ViewFeedbackPopUp.jsx file where we trigger the tip depending upon the feedback type.
> [!TIP]
> src/modules/feedback/containers/NewViewFeedbackContainer.jsx\
> src/modules/feedback/components/ViewFeedbackPopUp.jsx
