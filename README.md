# School-Management

The project is intended to contain the data of many teachers and students including their fee and funds in school.

School.java 
  
  public class School {

    private List<Teacher> teachers;
    private List<Student> students;
    private static int  totalMoneyEarned;
    private static int totalMoneySpent;

    /**
     * new school object is created.
     * @param teachers list of teachers in the school.
     * @param students list of students int the school.
     */
    public School(List<Teacher> teachers, List<Student> students) {
        this.teachers = teachers;
        this.students = students;
        totalMoneyEarned=0;
        totalMoneySpent=0;
    }
    
We use an ArrayList to declare and store the datas.

   public List<Teacher> getTeachers() {
        return teachers;
    }
  
It returns the list of teachers in the school.
  
  public void addTeacher(Teacher teacher) {
        teachers.add(teacher);
    }
  
Adds a teacher to the school.
  
  public List<Student> getStudents() {
        return students;
    }
  
Returns the list of students in the school.
  
  public void addStudent(Student student) {
        students.add(student);
    }
  
Adds a student to the school
  
  public int getTotalMoneyEarned() {
        return totalMoneyEarned;
    }
  
Returns the total money earned by the school.
  
  public static void updateTotalMoneyEarned(int MoneyEarned) {
        totalMoneyEarned += MoneyEarned;
    }
  
Adds the total money earned by the school.Money that is supposed to be  added.
  
  public int getTotalMoneySpent() {
        return totalMoneySpent;
    }
  
Returns the total money spent by the school.
  
  public static void updateTotalMoneySpent(int moneySpent) {
        totalMoneyEarned-=moneySpent;
     }
  
Updates the money that is spent by the school which is the salary given by the school to its teachers.
  
  
  
Student.java 
  
This class is responsible for keeping the track of students fees, name ,grade & fees paid.
  
  private int id;
    private String name;
    private int grade;
    private int feesPaid;
    private int feesTotal;
  
Declaring these variables in the class Student so as to use it further for storing data.
  
   public Student(int id, String name,int grade){
        this.feesPaid=0;
        this.feesTotal=30000;
        this.id=id;
        this.name=name;
        this.grade=grade;

    }
  
This is the constructor of the class. Creates a new student by initializing. Fees for every student is $30,000. Fees paid initially is 0.
  
  public void setGrade(int grade){
        this.grade=grade;
    }
  
Used to update the student's grade.
  
  public void payFees(int fees){
        feesPaid+=fees;
        School.updateTotalMoneyEarned(feesPaid);
    }
  
Keep adding the fees to feesPaid Field. Add the fees to the fees paid. The school is going to receive the funds.
  
  public int getId() {
        return id;
    }
  
Returns id of the student.
  
  public String getName() {
        return name;
    }
  
Returns name of the student.
  
  public int getGrade() {
        return grade;
    }
  
Returns the grade of the student.
  
   public int getFeesPaid() {
        return feesPaid;
    }
  
Returns the fees paid by the student.
  
  public int getFeesTotal() {
        return feesTotal;
    }
  
Returns the total fees of the student.
  
  public int getRemainingFees(){
        return feesTotal-feesPaid;
    }
  
Returns the remaining fees.
  

  
Teacher.java
  
This class is responsible for keeping the track of teacher's name, id, salary. It works same as Student class to add data such as getSalary(), getName(), salaryEarned().

  public class Teacher {

    private int id;
    private String name;
    private int salary;
    private int salaryEarned;

    /**
     * Creates a new Teacher object.
     * @param id id for the teacher.
     * @param name name of the teacher.
     * @param salary salary of the teacher.
     */
    public Teacher(int id, String name, int salary){
        this.id=id;
        this.name=name;
        this.salary=salary;
        this.salaryEarned=0;
    }

    /**
     *
     * @return the id of the teacher.
     */
    public int getId(){
        return id;
    }

    /**
     *
     * @return name of the teacher.
     */
    public String getName(){
        return name;
    }


    /**
     *
     * @return the salary of the teacher.
     */
    public int getSalary(){
        return  salary;
    }

    /**
     * set the salary.
     * @param salary
     */
    public void setSalary(int salary){
        this.salary=salary;
    }

    /**
     * Adds  to salaryEarned.
     * Removes from the total money earned by the school.
     * @param salary
     */
    public void receiveSalary(int salary){
        salaryEarned+=salary;
        School.updateTotalMoneySpent(salary);
    }


    @Override
    public String toString() {
        return "Name of the Teacher: " + name
                +" Total salary earned so far $"
                + salaryEarned;
    }
}
  
  
  
Main.java
  
In this class we declare the List and variables and finally print the results and output i.e the information of student, teacher as well as the school.
  


import java.util.ArrayList;
import java.util.List;


public class Main {
    public static void main(String[] args) {
        Teacher lizzy = new Teacher(1,"Lizzy",500);
        Teacher mellisa = new Teacher(2,"Mellisa",700);
        Teacher vanderhorn = new Teacher(3,"Vanderhorn",600);

        List<Teacher> teacherList = new ArrayList<>();
        teacherList.add(lizzy);
        teacherList.add(mellisa);
        teacherList.add(vanderhorn);


        Student tamasha = new Student(1,"Tamasha",4);
        Student rakshith = new Student(2,"Rakshith Vasudev",12);
        Student rabbi = new Student(3,"Rabbi",5);
        List<Student> studentList = new ArrayList<>();

        studentList.add(tamasha);
        studentList.add(rabbi);
        studentList.add(rakshith);




        School ghs = new School(teacherList,studentList);

        Teacher megan = new Teacher(6,"Megan", 900);

        ghs.addTeacher(megan);


        tamasha.payFees(5000);
        rakshith.payFees(6000);
        System.out.println("GHS has earned $"+ ghs.getTotalMoneyEarned());

        System.out.println("------Making SCHOOL PAY SALARY----");
        lizzy.receiveSalary(lizzy.getSalary());
        System.out.println("GHS has spent for salary to " + lizzy.getName()
        +" and now has $" + ghs.getTotalMoneyEarned());

        vanderhorn.receiveSalary(vanderhorn.getSalary());
        System.out.println("GHS has spent for salary to " + vanderhorn.getName()
                +" and now has $" + ghs.getTotalMoneyEarned());


        System.out.println(rakshith);

        mellisa.receiveSalary(mellisa.getSalary());

        System.out.println(mellisa);


    }
}
  
That is all for the project.
  
