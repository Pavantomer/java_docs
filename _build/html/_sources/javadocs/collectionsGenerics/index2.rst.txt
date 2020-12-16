**Collections & Generics-2**
=============================


**09. intro to Collections , List | array list**
-------------------------------------------------

9.1 Flow
----------
https://drive.google.com/open?id=0B5WQSHp6H2ZOZTVTN3RqSDR6eG8

9.2 Main Class
---------------

.. code-block::

    package com;
    import java.util.ArrayList;
    import java.util.Iterator;
    import java.util.List;

    public class Main {

        public static void main(String[] args) {
            ArrayListHelper a =new ArrayListHelper();
            a.createArrayList();


            Hospital h1 = new Hospital(002, "AIIMS", "South Delhi");
            Hospital h2 = new Hospital(235, "Safdarjung", "South-East Delhi");
            Hospital h3 = new Hospital(030, "Pentamed", "Model Town");

            List<Hospital> hospitalNames = new ArrayList<>();
            hospitalNames.add(h1);
            hospitalNames.add(h2);
            hospitalNames.add(h3);

            //for each example
            for (Hospital names : hospitalNames) {
                System.out.println(names);
            }

            // Iterator example
            System.out.println("All hospital : "  + hospitalNames);

            Iterator<Hospital> hIterator = hospitalNames.iterator();

            while(hIterator.hasNext()){

                Hospital hospital = hIterator.next();
                if(hospital.getId() > 10)
                    System.out.println(hospital);
                else
                    hIterator.remove();
            }
            System.out.println("After loop & condition : " + hospitalNames);
        }


    }


9.3 ArrayListHelper.java
--------------------------

.. code-block::

    package com;
    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.Iterator;
    import java.util.List;


    public class ArrayListHelper {
        private List<String> hospitalNames;

        public ArrayListHelper() {
            this.hospitalNames = null;
        }

        public List<String> getHospitalNames() {
            return hospitalNames;
        }

        public void setHospitalNames(List<String> hospitalNames) {
            this.hospitalNames = hospitalNames;
        }

        public void createArrayList() {
            
            List<String> hospitalNames = new ArrayList<>();

            // adding elements to list
            hospitalNames.add("BLK");
            hospitalNames.add("Max");
            hospitalNames.add("Fortis");
            hospitalNames.add("Apollo");
            hospitalNames.add("AIIMS");

            //sort arrayList
            Collections.sort(hospitalNames);

            //print list
            System.out.println("The names are : " + hospitalNames);

            //access via new for-loop
            for (String names : hospitalNames) {
                System.out.println(names);
            }

            //get size of arrayList
            int size = hospitalNames.size();
            System.out.println("Size of list is : " + size);

            //replace element from any index
            hospitalNames.set(2, "BLK Delhi");

            System.out.println("Element at index 2 replaced : " + hospitalNames);

            // check an element in list
            System.out.println("Is BLK in the list  : " + hospitalNames.contains("BLK"));

            //check if list is empty
            System.out.println("Is list empty : " + hospitalNames.isEmpty());

            //remove an element
            hospitalNames.remove(4);
            System.out.println(hospitalNames);

    //        //copying from one to another
    //        ArrayList<String> copyOfStringList = new ArrayList<String>();
    //        copyOfStringList.addAll(hospitalNames);
    //
    //        System.out.println("Copy of list : " + copyOfStringList);
    //
    //        Iterator<String> nameItertor = hospitalNames.iterator();
    //        while(nameItertor.hasNext()){
    //            System.out.println(nameItertor.next());
    //        }



        }
    }

9.4 Hospital.java
--------------------

.. code-block::

    package com;

    public class Hospital {
        private int id;
        private String name;
        private String location;

        public int getId() {
            return id;
        }
        public void setId(int id) {
            this.id = id;
        }
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        public String getLocation() {
            return location;
        }
        public void setLocation(String location) {
            this.location = location;
        }
        public Hospital(int id, String name, String location) {
            this.id = id;
            this.name = name;
            this.location = location;
        }
        @Override
        public String toString() {
            return "Hospital{" +
                    "id=" + id +
                    ", name='" + name + '\'' +
                    ", location='" + location + '\'' +
                    '}';
        }
    }


**10. Collections | Linked list**
----------------------------------

10.1 Links
-----------
https://drive.google.com/open?id=0B5WQSHp6H2ZOMlJzWlVsNUJUT0k

10.2 Main Class
-----------------

.. code-block::

    package com;

    public class Main {
        public static void main(String[] args) {

            AppointmentHelper app =new AppointmentHelper();

            app.CreateAppointment();
            app.ReadAppointment();
            app.UpdateAppointment();
            app.DeleteAppointment();
            
        }
    }

10.3 AppointmentHelper
-----------------------

.. code-block::

    package com;


    import java.util.LinkedList;
    import java.util.List;
    import java.util.ListIterator;

    public class AppointmentHelper  {

        List<Appointment> appointments = new LinkedList<>();


        //Create an appointment list
        public void CreateAppointment () {

            Appointment a1 = new Appointment("Ally",23);
            Appointment a2 = new Appointment("Sal",21);
            Appointment a3 = new Appointment("Murray", 45);
            Appointment a4 = new Appointment("Joe",89);

            appointments.add(a1);
            appointments.add(a2);
            appointments.add(a3);
            appointments.add(a4);
    //        System.out.println("LinkedList content: " + appointments);


        }

        //Read all the elements of the list using the iterator
        public void ReadAppointment() {
            System.out.println("LinkedList content: \n" + appointments.toString());

            ListIterator<Appointment> appointmentListIterator = appointments.listIterator();
            System.out.println("All the appointments in the list are :");
            while (appointmentListIterator.hasNext()) {
                System.out.println(appointmentListIterator.next());


            }
        }

        public void UpdateAppointment (){
            Appointment a = new Appointment("andy", 45);
            appointments.set(2,a);

            ListIterator<Appointment> appointmentListIterator = appointments.listIterator();
            System.out.println("Before after updation in the list are :");
            while (appointmentListIterator.hasNext()) {
                System.out.println(appointmentListIterator.next());
            }

        }


        //Delete an appointment at a particular index
        public void DeleteAppointment(){

            appointments.remove(0);
            System.out.println("Elements in the list after deleting are :");

            ListIterator<Appointment> appointmentListIterator = appointments.listIterator();
            while (appointmentListIterator.hasNext()){
                System.out.println( appointmentListIterator.next());
            }
        }



    }

10.4 Appointment.java
-----------------------

.. code-block::

    package com;



    import java.util.Objects;



    /**

    * Created by joy on 6/16/17.

    */

    public class Appointment {

        private String patientName;

        private int pId;



        public Appointment() {

            this.patientName = null;

            this.pId = 0;

        }



        public Appointment(String patientName, int pId) {

            this.patientName = patientName;

            this.pId = pId;

        }



        public String getPatientName() {

            return patientName;

        }



        public void setPatientName(String patientName) {

            this.patientName = patientName;

        }



        public int getpId() {

            return pId;

        }



        public void setpId(int appointmentNumber) {

            this.pId = appointmentNumber;

        }



        @Override

        public String toString() {

            return "Appointment{" +

                    "patientName='" + patientName + '\'' +

                    ", pId=" + pId +

                    '}';

        }



        @Override

        public boolean equals(Object o) {

            if (this == o) return true;

            if (o == null || getClass() != o.getClass()) return false;



            Appointment that = (Appointment) o;



            if (pId != that.pId) return false;

            return Objects.equals(patientName,pId);

        }



        @Override

        public int hashCode() {



            return Objects.hash(patientName,pId  );

        }

    }

**11. Collections | Stacks & queues**
--------------------------------------

11.1 Pdf link
---------------
https://drive.google.com/open?id=0B5WQSHp6H2ZONzI1amtLR193UUk

11.2 Main Class
----------------

.. code-block::

    /**

    * Created by joy on 5/30/17.

    */

    public class Main

    {

        public static void main(String[] args) {

            Stacks stacks = new ArrayStack();



            stacks.push(2);

            stacks.push(3);

            stacks.push(4);

            stacks.push(5);

            stacks.push(6);

            stacks.push(7);

            stacks.push(8);

            stacks.push(9);



            //TODO refractor this method later

            System.out.println(stacks);

    //        System.out.Returns a ResultSet object.println(stacks.pop());

            System.out.println(stacks.pop());

            System.out.println(stacks.peek());;

            stacks.push(888);

            System.out.println(stacks);



        }



        public String getHello() {

            return hello;

        }



        public void setHello(String hello) {

            this.hello = hello;

        }



        public String hello;

    }


11.3 Stacks.java
-----------------

.. code-block::

    /**

    * Created by joy on 5/30/17.

    * Stacks = LIFO

    * eg: stack of plates

    */

    public interface Stacks {



        public void push(Integer data);

        public Integer pop();

        public int getSize();

        public boolean isEmpty();

        public Integer peek();



    }
    
11.4 ArrayStack.java
---------------------

.. code-block::

    /**

    * Created by joy on 5/30/17.

    */

    public class ArrayStack implements Stacks{

        private int[] array;

        private int top = -1;

        private int size;



        public ArrayStack(int size){

            array = new int[size];



        }



        public ArrayStack(){

            array = new int[10];



        }



        public void push(Integer data) {

            if(top == array.length)

                reSize();

            top = top + 1;

            array[top] = data;

            size ++;

        }





        public Integer pop() {

            if(isEmpty())

                return null;

            int temp = array[top];

            top = top - 1;

            size --;

            return temp;

        }



        public int getSize() {

            return size;

        }



        public boolean isEmpty() {

            if(top == -1){

                return true;

            }

            else

            return false;

        }



        public Integer peek() {

            if(isEmpty())

            return null;

            else

                return array[top];

        }



        public void reSize(){

        int [] temp = new int[array.length * 2];

        for(int i = 0; i < array.length; i++){

            temp[i] = array[i];

        }

            array = temp;

        }



        public String toString(){

            String temp = "";

            for(int i = top ; i >= 0; i--){

                temp = temp + array[i] + "";

            }

            return temp;

        }

    }




