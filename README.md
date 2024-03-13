# Vue ToDo List App

This is a simple ToDo application built with Vue.js that allows users to manage their tasks. It has basic functionality to add task with date and time and also the completed task is shown on the app.

## Prerequisites

Before running the application, make sure you have the following installed:

- **Node.js**
- **JSON Server:** Install JSON Server globally using npm:
```bash
npm install json-server
```

## Getting Started

Follow these steps to run the application:

1. **Clone the github repository:**
```bash
git clone https://github.com/yadavikki/ToDo-App.git
```

2. **Navigate to the project directory:**

3. **Install dependencies:**
```bash
npm install
```

4. **Start the JSON Server:**

```bash
npx json-server --watch db.json --port 3000

```

5. **In a separate terminal, start the Vue.js development server:**

```bash
npm run serve

```


6. **Open your web browser and visit [http://localhost:8080](http://localhost:8080) to view the application.**

## Usage

- **Add a new task:** Type in the input field and click the "Add Task" button.It will be added to open tasks .
- **Mark tasks as completed:** Click the "Complete" button next to each task.Then it will be updated to complete task.



