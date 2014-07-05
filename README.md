planner
=======

version-1.0


import java.util.Scanner;

/**
A class that puts the amount of tasks in a list based on their category
@author Sneh Parmar
@version 1.1
*/

public class Planner {

    private static Scanner scan = new Scanner(System.in);

    /**
    @return A list of tasks that need to be completed each in its own category
    */

    public static void main(String[] args) {

        Task task1 = new Task("Exam 2", "CS 1331", 0);
        Task task2 = new Task("Startup Work", "Write Android code");
        Task task3 = new Task("Celebrate Birthday on the 19th with friends");

        ToDoList list1 = new ToDoList("College", task1);
        ToDoList list2 = new ToDoList("Startups", task2);
        ToDoList list3 = new ToDoList("Personal", task3);

        int checklist = 0;
        while (checklist != -1) {
            int remainingTasks = (list1.getNumTasks()
                - list1.getCompleteTasks()) + (list2.getNumTasks()
                - list2.getCompleteTasks()) + (list3.getNumTasks()
                - list3.getCompleteTasks());

            System.out.println("You have " + remainingTasks
                               + " unfinished tasks in 3 lists:");
            System.out.println("[0] " + "College\n" + "[1] " + "Startups\n"
                               + "[2] " + "Personal\n");
            System.out.print("Select a list to edit (or -1 to exit): ");

            checklist = scan.nextInt();
            System.out.println("\n");

            if (checklist == 0) {
                editList(list1);
            } else if (checklist == 1) {
                editList(list2);
            } else if (checklist == 2) {
                editList(list3);
            }
        }
    }

    /**
    @param list that is used to add or complete the tasks in each category
    @return A list of tasks that need to be completed each in its own category
    */
    private static void editList(ToDoList list) {

        System.out.println("\n" + list.toString() + "\n");

        int changelist = 0;
        while (changelist != -1) {
            System.out.println("[0] Add Task\n" + "[1] Complete Task\n"
                             + "[2] Complete All\n"
                             + "Select an option (or -1 to return): ");
            changelist = scan.nextInt();
            System.out.print("\n");

            if (changelist == 0) {
                System.out.println("Please enter a title: ");
                scan.nextLine();
                String taskName = scan.nextLine();
                System.out.println("Please enter any details: ");
                String taskDetails = scan.nextLine();
                System.out.println("Please enter a priority: ");
                Integer taskPriority = scan.nextInt();

                Task taskNew = new Task(taskName, taskDetails, taskPriority);
                list.add(taskNew);
            } else if (changelist == 1) {
                System.out.print("Which task have you completed: ");
                int completed = scan.nextInt();
                list.completeTask(completed);
            } else if (changelist == 2) {
                list.completeAll();
            }
            System.out.println(list.toString() + "\n");
        }
    }

}


