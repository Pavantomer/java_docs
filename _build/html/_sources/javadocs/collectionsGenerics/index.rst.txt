**Collections & Generics-1**
=============================

01. Generics
-------------
https://drive.google.com/open?id=18xkjoTYaAu0A2bBFkXQi_WUoFcUUdVC6

02. Working with Arrays
------------------------
https://drive.google.com/open?id=0B5WQSHp6H2ZOSHlOU3doNFFtcDA

03. Array Functions
--------------------
https://drive.google.com/open?id=1Iasfr3r3Th8WMLDOGR1QDzeSrYmSCC-F

04. Vector
----------
https://drive.google.com/open?id=18o1p-EwmQfqQRpUJomPtE2xR37Si7lXT

**05. Singly Linked list**
---------------------------

5.1 Pdf link
--------------
https://drive.google.com/open?id=0B5WQSHp6H2ZOcXRxTDhoRjEzTlk

5.2 Main class
----------------

.. code-block::

    package com;

    public class Main {

        public static void main(String[] args) {
    LinkedList linkedList = new LinkedList();

    linkedList.prepend(1);
    linkedList.prepend(23);
    linkedList.prepend(90);
    System.out.println("List after prepend : " + linkedList);

    linkedList.append(2);
    linkedList.append(34);
    linkedList.append(50);
    System.out.println("List after append : " + linkedList);

    linkedList.removeFirst();
            System.out.println("List after removing first element : " + linkedList);

    linkedList.removeLast();
            System.out.println("List after removing last element : " + linkedList);

        linkedList.insertAt(2,500);
            System.out.println("Insert " + linkedList);

        linkedList.removeAt(3);
            System.out.println("Remove at : " + linkedList);
            int sizeOfList = linkedList.getSize();
            System.out.println("The size of list is : " + sizeOfList);
        }
    }

5.3 LinkedList.java
--------------------
.. code-block::

    package com;

    /**

    * Created by joy on 6/14/17.

    */

    public class LinkedList extends Node{

        private Node header;

        private Node lastNode;

        private int size;



        public LinkedList(){

            header = new Node(null);

            lastNode = header;

        }

        //add node to beginning of list

        public void prepend(Integer data){

            Node n = new Node(data);

            //list is empty

            if(size == 0){

                header.next = n;

                lastNode = n;

                size ++;

            }

            //when list is not empty

            else {

                Node temp = header.next;

                header.next = n;

                n.next = temp;

                size++;

            }

        }

        //adding node at the end

        public void append(Integer data){

            Node n = new Node(data);

            //list is empty

            if(size == 0){

                header.next = n;

                lastNode = n;

                size ++;

            }

            else{

                lastNode.next = n;

                lastNode = n;

                size ++;

            }

        }

        public void removeFirst(){

            if(size != 0)

            header.next = header.next.next;

            size --;

        }



        public void removeLast(){

            if(size ==1){

                header.next = null;

                lastNode = header;

                size --;

            }

            else if(size != 0){

                Node n = header.next;

                int count = 1;

                while(count != size -1 ){

                    n = n.next;

                    count ++;

                }

                lastNode = n;

                lastNode.next = null;

                size --;

                }

        }



        public void insertAt(int index, int data){

            if(index <= 0 || index > size){

                return;

            }

            else if(index == 1){

                prepend(data);

            }

            else if (index == size){

                append(data);

            }

            else{

                Node n = new Node(data);

                Node x = header.next;

                int count = 1;

                while(count != index -1){

                    x = x.next;

                    count ++;

                }

                Node temp = x.next;

                x.next = n;

                n.next = temp;

                size ++;

            }



        }



        public void removeAt(int index){

            if(index <= 0 || index > size){

                return;

            }

            else if(index == 1){

                removeFirst();

            }

            else if (index == size){

                removeLast();

            }

            else{

                Node n = header.next;

                int count = 1;

                while(count != index - 1){

                    n = n.next;

                    count++;

                }

                n.next = n.next.next;

                size --;

            }

        }



        public int getSize(){

            return size;

        }

        public String toString(){

            Node n = header.next;

            String temp = " " ;

            while(n!= null){

                temp = temp + n.data + " ";

                n = n.next;

            }

            return temp;

        }





    }



5.4 Node.java
---------------

.. code-block::

    package com;



    /**

    * Created by joy on 6/14/17.

    */

    public class Node {

        protected Integer data;

        protected Node next;



        public Node(Integer data){

            this.data = data;

            next = null;

        }



        public Node() {

        }

    }


**06. Doublylinked List**
---------------------------

6.1 Pdf link
--------------
https://drive.google.com/open?id=0B5WQSHp6H2ZOWnRjZDIxcGpFd2M

6.2 DoublyLinkedList.java
---------------------------
.. code-block::

        package com;



        /**

        * Created by joy on 6/15/17.

        */

        public class DoublyLinkedList {

            private Node header;

            private Node lastNode;

            private int size;



            public DoublyLinkedList(){

                header = new Node(null);

                lastNode = header;

            }



            //add node to beginning of list

            public void prepend(Integer data){

                Node n = new Node(data);

                //list is empty

                if(size == 0){

                    header.next = n;

                    lastNode = n;

                    n.previous = header;

                    size ++;

                }

                else{

                    n.next = header.next;

                    n.previous = header;

                    header.next = n;

                    n.next.previous = n;

                    size ++;

                }

            }

            //adding node at the end

            public void append(Integer data){

                Node n = new Node(data);

                //list is empty

                if(size == 0) {

                    header.next = n;

                    lastNode = n;

                    n.previous = header;

                    size++;

                }

                else{

                    lastNode.next = n;

                    n.previous = lastNode ;

                    lastNode = n;

                    size ++;

                }

            }

            public void removeFirst(){

                if(size != 0)

                    header.next.next.previous = header;

                    header.next = header.next.next;

                size --;

            }



            public void removeLast(){

                if(size ==1){

                    header.next = null;

                    lastNode = header;

                    size --;

                }

                else if(size != 0){

                    lastNode = lastNode.previous;

                    lastNode.next = null;

                    size --;

                }

            }



            public void insertAt(int index, int data){

                if(index <= 0 || index > size){

                    return;

                }

                else if(index == 1){

                    prepend(data);

                }

                else if (index == size){

                    append(data);

                }

                else{

                    Node n = new Node(data);

                    Node x = header.next;

                    int count = 1;

                    while(count != index){

                        x = x.next;

                        count ++;

                    }

                    n.next = x;

                    n.previous = x.previous;

                    x.previous.next = n;

                    x.previous = n;

                    size ++;

                }



            }



            public void removeAt(int index){

                if(index <= 0 || index > size){

                    return;

                }

                else if(index == 1){

                    removeFirst();

                }

                else if (index == size){

                    removeLast();

                }

                else{

                    Node n = header.next;

                    int count = 1;

                    while(count != index){

                        n = n.next;

                        count++;

                    }

                    n.previous.next = n.next;

                    n.next.previous = n.previous;

                    size --;

                }

            }



            public int getSize(){

                return size;

            }

            public String toString(){

                Node n = header.next;

                String temp = " " ;

                while(n!= null){

                    temp = temp + n.data + " ";

                    n = n.next;

                }

                return temp;

            }



            public String reverseString(){

                Node n = lastNode;

                String temp = " " ;

                int tempSize = size;

                while(tempSize != 0){

                    temp = temp + n.data + " ";

                    n = n.previous ;

                    tempSize --;

                }

                return temp;

            }

        }


6.3 Main.Java
--------------

.. code-block::

    package com;



    public class Main {



        public static void main(String[] args) {

        DoublyLinkedList doublyLinkedList = new DoublyLinkedList();

        doublyLinkedList.prepend(2);

        doublyLinkedList.prepend(3);

        doublyLinkedList.prepend(4);

        doublyLinkedList.prepend(5);

        doublyLinkedList.prepend(6);

            System.out.println("prepend : " + doublyLinkedList);



        doublyLinkedList.append(10);

        doublyLinkedList.append(20);

        doublyLinkedList.append(30);

        doublyLinkedList.append(40);

        doublyLinkedList.append(50);



            System.out.println("append : " + doublyLinkedList);



        doublyLinkedList.removeFirst();

            System.out.println("removeFirst : " + doublyLinkedList);



        doublyLinkedList.removeLast();

            System.out.println("removeLast : " + doublyLinkedList);



        doublyLinkedList.insertAt(1,356);

            System.out.println("insertAt : " + doublyLinkedList);



        doublyLinkedList.removeAt(3);

            System.out.println("removeLast : " + doublyLinkedList);



            System.out.println("reverse string : " + doublyLinkedList.reverseString());



        }

    }


6.4 node.java
---------------

.. code-block::

    package com;



    /**

    * Created by joy on 6/15/17.

    */

    public class Node {

        protected Integer data;

        protected Node next;

        protected Node previous;



        public Node(Integer data){

            this.data = data;

            next = null;

            previous = null;

        }

    }


07. Stacks, Methods for stacks
-------------------------------
https://drive.google.com/open?id=0B5WQSHp6H2ZOVGJJaWhhRXE2a0k

**08. Queues, Methods for Queue**
-----------------------------------

8.1 Pdf link
---------------
https://drive.google.com/open?id=0B5WQSHp6H2ZOcDZqaVV2LTVqMTQ

8.2 Main Class
----------------

.. code-block::

    package com;



    public class Main {



        public static void main(String[] args) {

        Queue queue = new QueueArray();

        queue.enqueue(1);

        queue.enqueue(2);

        queue.enqueue(3);

        queue.enqueue(50);

        queue.enqueue(90);



            System.out.println(queue);



        queue.dequeue();

            System.out.println(queue);

        }

    }


8.3 Queue.java
---------------
.. code-block::

    package com;

    public class Main {



        public static void main(String[] args) {

        Queue queue = new QueueArray();

        queue.enqueue(1);

        queue.enqueue(2);

        queue.enqueue(3);

        queue.enqueue(50);

        queue.enqueue(90);



            System.out.println(queue);



        queue.dequeue();

            System.out.println(queue);

        }

    }

8.4 QueueArray.java
---------------------
.. code-block::

    package com;

    /**

    * Created by joy on 6/17/17.

    */

    public class QueueArray implements Queue{

        private int size;

        private int header = -1;

        private int tail = -1;

        private int[] array;



        public QueueArray(){

            array = new int[10];

        }



        public QueueArray(int size){



            array = new int[size];

        }



        @Override

        public void enqueue(int data) {

            if(isFull())

                reSize();

            if(isEmpty()){

                header = 0;

                tail = 0;

                array[0] = data;

                size++;

            }

            else {

                tail = (tail + 1) % array.length;

                array[tail] = data;

                size++;

            }

        }

        @Override

        public boolean isEmpty() {

            return size == 0;

        }



        @Override

        public boolean isFull() {

            return array.length == size;



        }



        @Override

        public int getSize() {

            return size;

        }





        public void reSize(){

            int[] temp = new int[array.length * 2];

            for(int i = 0; i < size; i++){

                temp[i] = array[(header + i) % array.length];

            }

            array = temp;

            header = 0;

            tail  = size - 1;

        }



        @Override

        public String toString() {

            String temp =  "" ;

            for(int i = 0; i < size; i++){

                temp = temp + array[(header + i) % array.length] + " ";

            }

            return temp;

        }



        @Override

        public Integer dequeue() {

            if (isEmpty())

                return null;

            else if (header == tail) {

                int temp = array[header];

                header = -1;

                tail = -1;

                size = 0;

                return temp;

            }

            else {

                int temp = array[header];

                header = (header + 1) % array.length;

                size--;

                return temp;

            }

        }

    }




