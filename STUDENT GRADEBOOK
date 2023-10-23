import java.io.*;
import java.util.*;

class Student {
    private String name;
    private int id;

    public Student(String name, int id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }
}

public class GradeManagementApp {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        Map<Integer, List<Integer>> gradeBook = new HashMap<>();

        loadStudentData(students, gradeBook);

        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. Add Student");
            System.out.println("2. Add Grade");
            System.out.println("3. Calculate Average Grade");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter student name: ");
                    String name = scanner.next();
                    System.out.print("Enter student ID: ");
                    int id = scanner.nextInt();
                    students.add(new Student(name, id));
                    gradeBook.put(id, new ArrayList<>());
                    saveStudentData(students, gradeBook);
                    break;
                case 2:
                    System.out.print("Enter student ID: ");
                    int studentId = scanner.nextInt();
                    System.out.print("Enter grade: ");
                    int grade = scanner.nextInt();
                    if (gradeBook.containsKey(studentId)) {
                        gradeBook.get(studentId).add(grade);
                        saveStudentData(students, gradeBook);
                    } else {
                        System.out.println("Student not found.");
                    }
                    break;
                case 3:
                    System.out.print("Enter student ID: ");
                    int calcStudentId = scanner.nextInt();
                    if (gradeBook.containsKey(calcStudentId)) {
                        List<Integer> grades = gradeBook.get(calcStudentId);
                        if (!grades.isEmpty()) {
                            double average = grades.stream().mapToInt(Integer::intValue).average().getAsDouble();
                            System.out.println("Average grade for Student " + calcStudentId + ": " + average);
                        } else {
                            System.out.println("Student has no grades.");
                        }
                    } else {
                        System.out.println("Student not found.");
                    }
                    break;
                case 4:
                    System.out.println("Goodbye!");
                    System.exit(0);
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    private static void loadStudentData(List<Student> students, Map<Integer, List<Integer>> gradeBook) {
        try (BufferedReader reader = new BufferedReader(new FileReader("student_data.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                String[] parts = line.split(",");
                if (parts.length == 2) {
                    students.add(new Student(parts[0], Integer.parseInt(parts[1]));
                    gradeBook.put(Integer.parseInt(parts[1]), new ArrayList<>());
                }
            }
        } catch (IOException e) {
            // Handle file not found or other I/O exceptions
        }
    }

    private static void saveStudentData(List<Student> students, Map<Integer, List<Integer>> gradeBook) {
        try (PrintWriter writer = new PrintWriter("student_data.txt")) {
            for (Student student : students) {
                writer.println(student.getName() + "," + student.getId());
            }
        } catch (IOException e) {
            // Handle file I/O exceptions
        }
    }
}
