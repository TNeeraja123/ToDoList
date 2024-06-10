# ToDoList
import tkinter as tk
from tkinter import messagebox

class TodoListApp:
    def _init_(self, root):
        self.root = root
        self.root.title("To-Do List")
        self.root.geometry("400x400")

        self.tasks = []

        self.create_widgets()

    def create_widgets(self):
        self.task_entry = tk.Entry(self.root, width=40)
        self.task_entry.pack(pady=10)

        add_task_btn = tk.Button(self.root, text="Add Task", command=self.add_task)
        add_task_btn.pack(pady=5)

        delete_task_btn = tk.Button(self.root, text="Delete Task", command=self.delete_task)
        delete_task_btn.pack(pady=5)

        clear_tasks_btn = tk.Button(self.root, text="Clear Tasks", command=self.clear_tasks)
        clear_tasks_btn.pack(pady=5)

        self.task_listbox = tk.Listbox(self.root, width=40, height=15, selectmode=tk.SINGLE)
        self.task_listbox.pack(pady=10)

    def add_task(self):
        task = self.task_entry.get()
        if task:
            self.tasks.append(task)
            self.task_listbox.insert(tk.END, task)
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "You must enter a task.")

    def delete_task(self):
        selected_task_index = self.task_listbox.curselection()
        if selected_task_index:
            task_index = selected_task_index[0]
            self.task_listbox.delete(task_index)
            del self.tasks[task_index]
        else:
            messagebox.showwarning("Warning", "You must select a task to delete.")

    def clear_tasks(self):
        self.task_listbox.delete(0, tk.END)
        self.tasks.clear()

if __name__ == "__main__":
    root = tk.Tk()
    app = TodoListApp(root)
    root.mainloop()
