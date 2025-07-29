import os

FILE_NAME = "todo.txt"

def load_tasks():
    if not os.path.exists(FILE_NAME):
        return []
    with open(FILE_NAME, "r") as file:
        tasks = file.read().splitlines()
    return tasks

def save_tasks(tasks):
    with open(FILE_NAME, "w") as file:
        file.write("\n".join(tasks))

def show_tasks(tasks):
    if not tasks:
        print("📝 Your to-do list is empty!")
    else:
        print("\n📋 To-Do List:")
        for idx, task in enumerate(tasks, start=1):
            print(f"{idx}. {task}")
    print()

def add_task(tasks):
    task = input("Enter a new task: ")
    tasks.append(task)
    print("✅ Task added successfully.")

def delete_task(tasks):
    show_tasks(tasks)
    try:
        num = int(input("Enter task number to delete: "))
        if 1 <= num <= len(tasks):
            removed = tasks.pop(num - 1)
            print(f"🗑️ Task '{removed}' deleted.")
        else:
            print("⚠️ Invalid task number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

def update_task(tasks):
    show_tasks(tasks)
    try:
        num = int(input("Enter task number to update: "))
        if 1 <= num <= len(tasks):
            new_task = input("Enter the updated task: ")
            tasks[num - 1] = new_task
            print("🔄 Task updated.")
        else:
            print("⚠️ Invalid task number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

def main():
    tasks = load_tasks()

    while True:
        print("\n==== TO-DO LIST MENU ====")
        print("1. Show Tasks")
        print("2. Add Task")
        print("3. Delete Task")
        print("4. Update Task")
        print("5. Exit")
        choice = input("Choose an option (1-5): ")

        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            delete_task(tasks)
        elif choice == "4":
            update_task(tasks)
        elif choice == "5":
            save_tasks(tasks)
            print("💾 Tasks saved. Goodbye!")
            break
        else:
            print("⚠️ Invalid choice. Please select between 1 to 5.")

if __name__ == "__main__":
    main()
