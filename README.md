# Mobile app simple prototype

## OTP Authentication Flow

**Description**:  
The OTP (One-Time Password) authentication allows users to sign in securely using their phone number and a PIN code. The process consists of two HTTP requests, which are handled in a step-by-step flow as described below.

1. **Send OTP Request**  
   - When the user enters their phone number, initiate an HTTP request to send an OTP to their device.  
   - API Endpoint: [Send OTP Request](https://www.postman.com/orange-meteor-329457/new-team-workspace/request/0fz0fj3/authenticate-sms?action=share&creator=33185536&ctx=documentation).  
   - On successful request, show the **PIN Input Screen** where the user can enter the received OTP.

2. **Validate OTP & Sign In**  
   - Once the user enters the OTP, send an HTTP request to validate the OTP along with the phone number.  
   - API Endpoint: [Validate OTP and Sign In](https://www.postman.com/orange-meteor-329457/new-team-workspace/request/h3ihsda/sign-in-copy?action=share&creator=33185536&ctx=documentation).  
   - If the OTP is correct, the server responds with a **User Object** containing the authentication token and a list of the user’s accounts.  

3. **Save User Data to Local Database**  
   - Store the received user data (user with token and accounts) in a local database (users table).
   - Use **React Context** (not Redux) to manage the user’s basic information throughout the app.
   - On subsequent app launches, check the local database for a logged-in user to skip the authentication screens if the user is already authenticated.

---

### Calendar Module

**Description**:  
The calendar is a custom-built component designed to display lessons in a user-friendly format using UNIX timestamp integers for date management.

1. **Monthly and Daily Views**  
   - The calendar displays a **list of months** and the **days in the selected month**.
   - When a specific day is selected, the **lessons** for that day are displayed.

2. **Lesson Details**  
   - Clicking on a specific lesson opens a detailed view of the lesson.  
   - API Endpoint: [Get Lesson Info](https://www.postman.com/orange-meteor-329457/new-team-workspace/request/3bgmc71/lesson?action=share&creator=33185536&ctx=documentation).

3. **Create Lesson**  
   - The calendar screen has a **button to create a new lesson**, which opens a bottom sheet.
   - In the bottom sheet, users can specify lesson details (e.g., clients, date, time, and duration).  
   - Use **pseudo API requests** for lesson creation (as the actual API is still under development). You can later uncomment these parts of the code once the API is ready.
   - Nested bottom sheets allow users to select clients and set other lesson parameters dynamically.

---

### Client Management

**Description**:  
The app features a comprehensive client management module where users can view, create, and manage clients.

1. **View Clients**  
   - The **Client List** screen displays all saved clients.  
   - API Endpoint: [Get All Clients](https://www.postman.com/orange-meteor-329457/new-team-workspace/request/6y7q1fl/get-all-clients?action=share&creator=33185536&ctx=documentation).
   
2. **Client Details**  
   - Clicking on a specific client opens a detailed view displaying their basic information.  
   - API Endpoint: [Get Client Info](https://www.postman.com/orange-meteor-329457/new-team-workspace/request/q8nhalq/get-client?action=share&creator=33185536&ctx=documentation).

3. **Create Client**  
   - The **Client List** screen also contains a "plus" button to add a new client.
   - This opens a bottom sheet where users can fill in the basic client details (e.g., name, contact info).  
   - API Endpoint: [Create Client](https://www.postman.com/orange-meteor-329457/new-team-workspace/request/ng8uwui/create-client?action=share&creator=33185536&ctx=documentation).
   - Upon submission, an HTTP request will create the client and save it to the database.

---

### Account Management

**Description**:  
The **Account** screen provides users with essential account management options and functionalities.

1. **Account Information**  
   - Display user information like privacy settings and provide options to **edit account details**.
   
2. **Switch Between Accounts**  
   - The user can switch between their different accounts (retrieved during the OTP sign-in) directly from the account screen.

3. **Logout**  
   - Provide an option to log out from the app, which will also clear the user's data from the local database.

4. **Delete Account**  
   - An option to delete the user account should be available, with appropriate warnings before action.
