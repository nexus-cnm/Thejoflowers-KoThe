flowchart TD
  Start[Start] --> CheckAuth{User Authenticated}
  CheckAuth -- Yes --> ShowHome[Show Home Page]
  CheckAuth -- No --> ShowLogin[Show Login Page]
  ShowLogin --> LoginSubmit[User submits login form]
  LoginSubmit --> LoginCheck{Login successful}
  LoginCheck -- Yes --> ShowHome
  LoginCheck -- No --> ShowLoginError[Show login error]
  ShowHome --> Navigation[User navigates]
  Navigation -- Tasks --> LoadTasks[Load Tasks List]
  LoadTasks --> InertiaRequest[Inertia XHR request to Tasks index route]
  InertiaRequest --> ControllerIndex[Controller tasks index action]
  ControllerIndex --> FetchTasks[Fetch tasks from database]
  FetchTasks --> InertiaResponse[Return Inertia response with tasks data]
  InertiaResponse --> TasksPage[Render tasks index page]
  TasksPage -- Create --> ShowCreate[Show create task form]
  ShowCreate --> SubmitCreate[User submits create form]
  SubmitCreate --> ControllerStore[Controller tasks store action]
  ControllerStore --> SaveTask[Save task to database]
  SaveTask --> InertiaResponseCreate[Return Inertia response after create]
  InertiaResponseCreate --> TasksPage
  TasksPage -- Edit --> ShowEdit[Show edit task form]
  ShowEdit --> SubmitEdit[User submits edit form]
  SubmitEdit --> ControllerUpdate[Controller tasks update action]
  ControllerUpdate --> UpdateTask[Update task in database]
  UpdateTask --> InertiaResponseUpdate[Return Inertia response after update]
  InertiaResponseUpdate --> TasksPage
  TasksPage -- Delete --> DeleteAction[User triggers delete task]
  DeleteAction --> ControllerDelete[Controller tasks delete action]
  ControllerDelete --> RemoveTask[Remove task from database]
  RemoveTask --> InertiaResponseDelete[Return Inertia response after delete]
  InertiaResponseDelete --> TasksPage
  ShowHome -- Logout --> LogoutAction[User clicks logout]
  LogoutAction --> ControllerLogout[Controller logout action]
  ControllerLogout --> InertiaResponseLogout[Return Inertia response after logout]
  InertiaResponseLogout --> ShowLogin