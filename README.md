# ChatApp 💬

## Overview ℹ️
ChatApp is a real-time chat application designed to connect people and groups based on specific unique IDs (UIDs). Unlike traditional messaging apps, ChatApp prioritizes user privacy by not requiring phone number verification. Instead, it utilizes email verification, allowing users to maintain separation between their public and personal lives while respecting their privacy.

## Features ✨
- Unique ID-based connections: Users can connect with individuals and groups based on specific unique IDs.
- Email verification: Ensures user authenticity while respecting privacy by utilizing email verification instead of phone numbers.
- Real-time messaging: Users can send and receive messages instantly.
- Authentication: Users can sign up, log in, and securely authenticate using Auth0.
- Persistent storage: Messages are stored in MongoDB for persistence.
- Cross-origin resource sharing: CORS is implemented for secure communication between client and server.

## Technologies Used 🛠️
- React: Frontend framework for building user interfaces.
- Node.js: JavaScript runtime environment for backend development.
- Express: Web application framework for Node.js.
- MongoDB: NoSQL database for storing chat messages.
- Auth0: Authentication and authorization platform.
- Socket.IO: Library for real-time, bidirectional communication between web clients and servers.
- CORS (Cross-Origin Resource Sharing): Mechanism for secure cross-origin requests.

## Installation 🚀
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/ChatApp.git
   cd ChatApp

#### Run the Backend:
2.  ```bash
    cd chatappbackend
    cp .sample.env .env
    npm install 
    npm start

### Run the frontend:
3. ```bash
   cd chatappfrontend
   cp .sample.env .env
   npm install 
   npm run dev 

# Backend 🗄️

## Backend DataBase Schema && LLD Design 📐

![Alt text](<DB.png>)

## Node Modules Functions: 🔧


#### UID.js

- **checkUid(uid)**: Checks if a UID is present in MongoDB.
- **findNameByUid(input)**: Finds a name associated with a UID, email, or name.
- **replaceUid(oldUid, newUid)**: Replaces an old UID with a new UID.
- **checkUidByEmailAndName(email, name)**: Checks UID based on email and name.

#### Group.js

- **createGroup(Name, memberEmails, groupUid)**: Creates a new group with the provided name, member emails, and group UID.
- **addMemberToGroup(groupID, groupUid, memberIdentifier)**: Adds a member to a group by email or UID.
- **findGroupNameByIdOrName(groupUid, groupName)**: Finds a group's name by group UID or name.
- **addUserToGroup(userUid, userName, groupUid)**: Adds a user to a group by UID, name, and group UID.


#### Auth.js

- **connectToMongoDB()**: Connects to MongoDB using the provided MONGO_URL from environment variables.
- **uploadUser(name, email, uid)**: Uploads user data with name, email, and UID to the database.
- **User**: MongoDB model representing a user with fields for name, email, and UID.

#### Email.js

- **checkUserEmailInMongoDB(email)**: Checks if a user's email exists in MongoDB.
- **getUserEmailByUid(uid)**: Retrieves a user's email by UID.


#### Contacts.js

- **createOrUpdateContact(contacts, uid)**: Creates or updates a contact in the database with the provided contacts array and UID.
- **addContact(uid, contactName, contactId)**: Adds a contact to a user with the given UID, contact name, and contact ID.
- **provideUidforNames(uid)**: Retrieves names associated with a UID from the database.


#### SocketUser.js

- **setupWebSocketServer(server)**: Sets up a WebSocket server using Socket.io on the provided HTTP server. Handles events for sending and receiving messages between clients.


#### Messages.js

- **uploadMessage(concatenatedIds, message, isReceived)**: Uploads a received or sent message to the database.
- **fetchMessages(concatenatedIds)**: Fetches messages sorted by timestamp for the provided concatenated IDs.






# Frontend(React) 📺

## Homepage 🏠
![Homepage](<temp2.png>)

## Auth0 🔒
![Auth0](<Auth0.png>)

## ChatWindow 🐦🪟
![ChatWindow](<temp1.png>)

![ChatWindow](<temp3.png>)

## Home Component

The `Home` component represents the main landing page of the application. It includes a navigation bar, sections for About, Features, and Contact, and a section for claiming a username and entering the chat.

### Dependencies

- `React`: React library for building user interfaces.
- `@auth0/auth0-react`: Auth0 library for handling authentication.
- `react-router-dom`: React Router library for declarative routing.
- `../CompStyles/Home.css`: CSS file for styling the home page.
- `Navbar.jsx`: Component for rendering the navigation bar.
- `About.jsx`: Component for rendering the About section.
- `Feature.jsx`: Component for rendering the Features section.
- `Contact.jsx`: Component for rendering the Contact section.



## VerNavbar Component

The `VerNavbar` component is a vertical navigation bar used in the application. It allows users to perform various actions such as adding groups, searching for users, changing UID, and logging out. Additionally, it displays selected users and fetched names.

### Props

- `onSelectUserName`: A function to handle the selection of a user's name.
- `onSelectCurruid`: A function to handle the selection of the current UID.

### Dependencies

- `React`: React library for building user interfaces.
- `PropTypes`: Library for typechecking React props.
- `@auth0/auth0-react`: Auth0 library for handling authentication.
- `react-icons/fa`: FontAwesome icons for React.
- `AddChatModal.jsx`: Component for adding a chat modal.
- `SearchModal.jsx`: Component for search modal.
- `AddUidModal.jsx`: Component for adding UID modal.
- `LogoutModal.jsx`: Component for logout modal.
- `../CompStyles/VerNavbar.css`: CSS file for styling the vertical navbar.
- `NewsCrawl.jsx`: Component for news crawl.

## AddChatModal Component

The `AddChatModal` component is a modal used for adding a new chat group. It allows users to input a group name, member email, and group UID, and then submit to create the group.

## SearchModal Component

The `SearchModal` component is a modal used for searching users or groups based on their UID, name, or group name. It allows users to input a search query and retrieve search results.



## AddUidModal Component

The `AddUidModal` component is a React component used to display a modal for adding or updating a user's UID (Unique Identifier). It utilizes the Auth0 authentication library for handling user authentication and interacts with an API to fetch and save UID data.


## ChatApp Component

The `ChatApp` component serves as the main container for the chat application. It manages the state and rendering of various subcomponents based on user interactions and screen size.

### Props

- `userEmail`: The email of the current user.

### Dependencies

- `React`: React library for building user interfaces.
- `./VerNavbar`: The vertical navigation bar component.
- `./ChatWindow`: The chat window component.
- `./NoUidModal`: The modal component for handling cases where the user's UID is not found.
- `../CompStyles/ChatApp.css`: CSS file for styling the chat application.


## ChatWindow Component

The `ChatWindow` component represents the main chat window where users can send and receive messages.

### Props

- `selectedUserName`: An array containing the selected user's name and UID.
- `currUid`: The UID of the current user.
- `setShowChatWindow`: A function to control the visibility of the chat window.

### Dependencies

- `React`: React library for building user interfaces.
- `@auth0/auth0-react`: Library for authentication using Auth0.
- `../CompStyles/ChatWindow.css`: CSS file for styling the chat window.
- `react-icons/fa`: FontAwesome icons for UI elements.
- `socket.io-client`: Client-side library for WebSocket communication.
- `./NewsCrawl`: Component for displaying news feed.







