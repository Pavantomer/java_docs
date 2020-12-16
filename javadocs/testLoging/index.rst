**Testing & Logging**
+++++++++++++++++++++


01. Exceptions , Class Hierarchy and Exception Handling, Using try-catch block,finally Try-With-Resources
---------------------------------------------------------------------------------------------------------
https://drive.google.com/open?id=0B5WQSHp6H2ZOa1JZenFaNWpUVHc

**02. Custom Exception**
------------------------

2.1 Flow
--------

link : https://bitbucket_datreon@bitbucket.org/datreon/custom-exception.git

2.2 Main class
--------------
.. code-block::

        public class Main {


            public static void main(String[] args) {

                String situation   = "unknown Case" ;

                try {
                    if ( situation.isEmpty()) {
                        System.out.println("its empty");
                    }
                    else if (situation.equals("unknown Case")) {

                        throw( new CustomException());

                    }
                } catch (CustomException e) {
                    e.printStackTrace();
                }
            }

        }


2.3 CustomException.java
-------------------------

.. code-block::

        public class CustomException extends Exception {
            public static final long serialVersionUID = 1234L;
            public CustomException(){
                System.out.println("this is custom exception being tackled ");
            }
        }

03. Unit Testing , Junit4
---------------------------

https://drive.google.com/open?id=0B5WQSHp6H2ZOSnRROTc4ZWJYQjQ

04. Log4j*
----------

4.1 Flow
---------
Link : https://drive.google.com/open?id=0B5WQSHp6H2ZOdWVsMVYtaHZSbTA

4.2 Main Class
--------------

.. code-block::

        public class Main {
            public static void main(String[] args) {
                Calculator calculator = new Calculator();

                calculator.inputNumbers();

                int addAns = calculator.add();
                System.out.println(addAns);

                int subtractAns = calculator.subtract();
                System.out.println(subtractAns);

                int multiplyAns = calculator.multiply();
                System.out.println(multiplyAns);

                int divideAns = calculator.divide();
                System.out.println(divideAns);
            }
        }


4.3 pom.xml
-----------

.. code-block::

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>com</groupId>
        <artifactId>calculatorWithLogging</artifactId>
        <version>1.0-SNAPSHOT</version>

        <dependencies>
            <dependency>
                <groupId>org.apache.logging.log4j</groupId>
                <artifactId>log4j-core</artifactId>
                <version>2.7</version>
            </dependency>

            <dependency>
                <groupId>org.apache.logging.log4j</groupId>
                <artifactId>log4j-api</artifactId>
                <version>2.7</version>
            </dependency>
        </dependencies>


    </project>


4.4 log4j2.xml
---------------
.. code-block::

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
        <param name="ConversionPattern" value=""/>
        <appenders>
            <Console name="Console" target="SYSTEM_OUT">
                <PatternLayout pattern="\t%d{HH:mm:ss.SSS} %-5p - [%-m] - at %c.%M(%F:%L)%n "/>
            </Console>

            <File name="LogFile" fileName="logs/app.log">
                <PatternLayout pattern="%d{yyyy-mm-dd HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
            </File>
        </appenders>

        <loggers>
            <root level="trace">
                <appender-ref ref="Console" />
                <appender-ref ref="LogFile" />
            </root>
        </loggers>
    </configuration>

4.5 Calculator.java
-------------------
.. code-block::

    import org.apache.logging.log4j.LogManager;
    import org.apache.logging.log4j.Logger;

    import java.util.Scanner;


    public class Calculator {

        private static final Logger LOG = LogManager.getLogger(Calculator.class);
        private int num1,num2,choice;
        private double answer;

        public Calculator() {
            this.num1 = 0;
            this.num2 = 0;
            this.choice = 0;

            LOG.info("Calculator Initialized num1 = {} num2 = {}",num1,num2);
        }

        public int getNum1() {
            return num1;
        }

        public void setNum1(int num1) {
            this.num1 = num1;
        }

        public int getNum2() {
            return num2;
        }

        public void setNum2(int num2) {
            this.num2 = num2;
        }

        public int getChoice() {
            return choice;
        }

        public void setChoice(int choice) {
            this.choice = choice;
        }

        public void inputNumbers(){
            System.out.println("Enter number1 : ");
            Scanner inputNum1 = new Scanner(System.in);
            num1 = inputNum1.nextInt();
            System.out.println("Enter number2 : ");
            Scanner inputNum2 = new Scanner(System.in);
            num2 = inputNum2.nextInt();
        }

        public int add(){
            LOG.info("Add method Called");
            return num1+num2;
        }

        public int subtract(){
            LOG.info("Subtract method Called");
            return num1-num2;
        }

        public int divide(){
            LOG.info("Divide method Called");

            int result = 0;

            if(num2 == 0){
                try {
                    result = num1/num2;
                }
                catch (Exception e){
                    LOG.warn("Divide by zero = " + e.toString());
                }
            }
            return result;
        }

        public int multiply(){
            LOG.info("Multiply method Called");
            return num1*num2;
        }
    }

**5. Logger**
---------------
5.1 Link
---------
link : https://drive.google.com/open?id=0B5WQSHp6H2ZOSm85emNXOERjUEU

5.2 Main class
---------------

.. code-block::

    public class Main {


        public static void main(String[] args) {


                //objects
                logA A = new logA();
                logB B = new logB();
                logC C = new logC();

    //        loggerMain.log(Level.INFO ,"this is a test ");
                A.printA();

                B.printB();

                C.printC();

        }

    }

5.3 logA.java
--------------

.. code-block::

    import java.io.IOException;
    import java.util.logging.FileHandler;
    import java.util.logging.Handler;
    import java.util.logging.Level;
    import java.util.logging.Logger;


    public class logA  {
        private  static  Handler fileHandler  ;
        private final Logger loggerA = Logger.getLogger(logA.class.getName());

        public void printA(){
            try {
                fileHandler = new FileHandler("/home/div/log.txt");
                loggerA.addHandler(fileHandler);

            System.out.println("log A");
            //Logging A
            loggerA.log(Level.INFO, "logger class A");
    //        loggerA.info("logger Class A");
            }catch (IOException e){
                e.printStackTrace();

            }
        }
    }

5.4 logB.java
--------------

.. code-block::

    import java.util.logging.Logger;


    public class logB {


        private final Logger loggerB = Logger.getLogger("logB");

        public void printB(){

            System.out.println("log B");
            //Logging B
            loggerB.info("logger Class B");
        }
    }

5.5 logC.java
--------------
.. code-block::

    import java.util.logging.ConsoleHandler;
    import java.util.logging.Logger;

    public class logC {

    //    private  static ConsoleHandler consoleHandler ;
        private final Logger loggerC = Logger.getLogger(logC.class.getName());


        public void printC(){

    //        loggerC.addHandler(new ConsoleHandler());

            System.out.println("log C");
            //Logging C
            loggerC.info("logger Class C");
        }
    }


