# to-do-project
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Task class to represent individual tasks
class Task {
private:
    string description;
    bool isComplete;

public:
    Task(const string& desc) : description(desc), isComplete(false) {}

    // Get task description
    string getDescription() const {
        return description;
    }

    // Check if task is complete
    bool isTaskComplete() const {
        return isComplete;
    }

    // Set task as complete
    void completeTask() {
        isComplete = true;
    }

    // Display task details
    void displayTask() const {
        cout << (isComplete ? "[Done] " : "[Pending] ") << description << std::endl;
    }
};

// ToDoList class to manage tasks
class ToDoList {
private:
    vector<Task> tasks;

public:
    // Add task to the list
    void addTask(const std::string& taskDescription) {
        tasks.push_back(Task(taskDescription));
    }

    // Remove task from the list
    void removeTask(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks.erase(tasks.begin() + index);
        }
    }

    // Mark a task as complete
    void completeTask(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks[index].completeTask();
        }
    }

    // Display all tasks
    void displayAllTasks() const {
        if (tasks.empty()) {
            std::cout << "Your To-Do list is empty!" << std::endl;
            return;
        }
        for (int i = 0; i < tasks.size(); ++i) {
            std::cout << i + 1 << ". ";
            tasks[i].displayTask();
        }
    }
};

//Main function
int main() {
    ToDoList myToDoList;
    int choice;
    std::string taskDescription;
    int taskIndex;

    do {
        cout << "\nTo-Do List Menu:\n";
        cout << "1. Add Task\n";
        cout << "2. Remove Task\n";
        cout << "3. Mark Task as Complete\n";
        cout << "4. Show All Tasks\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore();  // to ignore any leftover newline from the previous input

        switch (choice) {
            case 1:
               cout << "Enter task description: ";
               getline(std::cin, taskDescription);
                myToDoList.addTask(taskDescription);
                break;
            case 2:
               cout << "Enter task number to remove: ";
              cin >> taskIndex;
                myToDoList.removeTask(taskIndex - 1); // subtract 1 for 0-based index
                break;
            case 3:
              cout << "Enter task number to mark as complete: ";
               cin >> taskIndex;
                myToDoList.completeTask(taskIndex - 1); // subtract 1 for 0-based index
                break;
            case 4:
                myToDoList.displayAllTasks();
                break;
            case 5:
                cout << "Exiting the To-Do List program. Goodbye!" << std::endl;
                break;
            default:
                cout << "Invalid choice! Please try again." << std::endl;
        }

    } while (choice != 5);

    return 0;
}
