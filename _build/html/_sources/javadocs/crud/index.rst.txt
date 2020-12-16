**CRUDs**
==========

01. File IO code
------------------

1.1 Flow
---------
https://drive.google.com/open?id=0B5WQSHp6H2ZOQUdwNEh6eDlWR0U

Clone code from repo

$  https://bitbucket_datreon@bitbucket.org/datreon/file-io.git

1.2 Main Class
---------------

.. code-block::

    import java.io.IOException;


    public class Main {
        public static void main(String[] args) throws IOException {



            CRUD_FileIO CRUDFileIO = new CRUD_FileIO();

            CRUDFileIO.creatingFile();

            CRUDFileIO.inputFilePath();


            CRUDFileIO.writingFile();
            CRUDFileIO.reading();

            CRUDFileIO.appendFile();

            //comment this line to avoid deletion after creation
            CRUDFileIO.deleteFile();

    //        CRUDFileIO.setData("File IO ");
    //        CRUDFileIO.setFilePath("/home/datreon/sample.txt");

        }
    }


1.3 CRUD_FileIO Class
----------------------

.. code-block::

    import java.io.*;
    import java.nio.file.Files;
    import java.nio.file.NoSuchFileException;
    import java.util.Scanner;

    public class CRUD_FileIO extends  FilePath {

        //private String filePath;
        private String data;
        private boolean check;

        public CRUD_FileIO(){
            //filePath = null;
            data  = null;
            check = Boolean.parseBoolean(null);
        }


        public String getData(){
            return data;
        }

        public void setData(String data){
            this.data = data;
        }
        //create new file 
        public void creatingFile() throws IOException {

            File file = new File(inputFilePath());
            boolean check = file.createNewFile();

            if (check == true){
                System.out.println("File is created!");
            }else{
                System.out.println("File already exists.");
            }
        }


        //read an existing file
        public void reading() throws IOException{

            try {
                FileReader fileReader = new FileReader(outputFilePath());
                BufferedReader bufferedReader = new BufferedReader(fileReader);

                String line;
                while((line = bufferedReader.readLine())!= null)
                {
                    System.out.println(line);
                }

                bufferedReader.close();

            }
            catch (FileNotFoundException e){
                e.printStackTrace();
            }

        }


        /writing to file 
        public void writingFile() throws IOException {
            System.out.println(" please enter the data to be written to file ");

            try {
            Scanner dataInput = new Scanner(System.in);

            data = dataInput.nextLine();

                FileWriter fileWriter = new FileWriter(outputFilePath());

                BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);

                bufferedWriter.write(data);
                bufferedWriter.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        //update 
        public void appendFile() throws IOException {

            //add data to append
            System.out.println("Add the additional data : ");
            Scanner addData = new Scanner(System.in);
            String additionalData = addData.nextLine();

            FileWriter fileWriter1 = new FileWriter(inputFilePath(), true);
            BufferedWriter bufferedWriter1 = new BufferedWriter(fileWriter1);

            PrintWriter pw = new PrintWriter(bufferedWriter1);
            pw.println(additionalData);
            pw.close();

            System.out.println("Data successfully appended at the end of file");
        }

            public void deleteFile () throws IOException {;

                try {
                    File file =new  File(deleteFilePath());
                    file.delete();
                    setOutputFilePath("File Deleted Successfully ");

                } catch (Exception e) {
                    e.printStackTrace();
                }


            }
    }

1.4 FilePath class
-------------------

.. code-block::

    import java.util.Scanner;


    public class FilePath {
        private  String inputFilePath ;
        private  String outputFilePath;
        private  String deleteFilePath;

        public String getInputFilePath() {
            return inputFilePath;
        }

        public String getOutputFilePath() {
            return outputFilePath;
        }

        public void setInputFilePath(String inputFilePath) {
            this.inputFilePath = inputFilePath;
        }

        public void setOutputFilePath(String outputFilePath) {
            this.outputFilePath = outputFilePath;
        }


        public String  inputFilePath()
        {

            System.out.println("Enter path along with name of file you want to create : ");
            Scanner inputFileLocation = new Scanner(System.in);
            inputFilePath = inputFileLocation.next();
            return inputFilePath;

        }

        public String outputFilePath()
        {

            System.out.println("Enter path along with name of file you want to read : ");
            Scanner outputFileLocation = new Scanner(System.in);
            outputFilePath = outputFileLocation.next();
            return outputFilePath;

        }

        public String deleteFilePath()
        {

            System.out.println("Enter path along with name of file you want to delete : ");
            Scanner deleteFileLocation = new Scanner(System.in);
            deleteFilePath = deleteFileLocation.next();
            return deleteFilePath;

        }

    }

02. JDBC Code
----------------

2.1 pom.xml
-------------

.. code-block::

    <dependencies>

            <dependency>

                <groupId>mysql</groupId>

                <artifactId>mysql-connector-java</artifactId>

                <version>6.0.5</version>

            </dependency>

        </dependencies>


2.2 Flow
-----------

Doc link :https://drive.google.com/open?id=0B5WQSHp6H2ZOY1V5bURmQU9pcGM

Docker run mysql statement :

docker run --name mysqlTest -d -p 3306:3306 --env="MYSQL_DATABASE=test" --env="MYSQL_ROOT_PASSWORD=Qwerty@321" --env="MYSQL_USER=datreon"--env="MYSQL_PASSWORD=Qwerty@321" mysql --bind_address=0.0.0.0



Expose the port 3306 in virtual box over the nat network



Clone the bitbucket repo

$   https://bitbucket_datreon@bitbucket.org/datreon/jdbc-crud.git


2.3 Main Class
----------------

.. code-block::

    import java.sql.SQLException;

    public class Main {

        public static void main(String[] args) throws SQLException {



            CrudJdbcWithStatement crudJdbcWithStatement = new CrudJdbcWithStatement();



    //        crudJdbcWithStatement.setJdbcurl("jdbc:mysql://192.168.100.44:3306/test");

    //        crudJdbcWithStatement.setUsername("root");

    //        crudJdbcWithStatement.getUsername();

    //        crudJdbcWithStatement.setPassword("Qwerty@321");



            crudJdbcWithStatement.enterConnectionDetails();

            crudJdbcWithStatement.makeConnection();



            crudJdbcWithStatement.setCreateTableSQL("CREATE TABLE  Users"+

                    "(" +

                    "    id INT(11), " +

                    "    name VARCHAR(255)," +

                    "    age INT(11)," +

                    "    email VARCHAR(255)" +

                    ")" );

            crudJdbcWithStatement.createTable();



            crudJdbcWithStatement.insertRow();

            crudJdbcWithStatement.readTable();



            crudJdbcWithStatement.updateRow(11, 22);



            crudJdbcWithStatement.readTable();

            crudJdbcWithStatement.deleteRow(3);

        }

    }

2.4 ConnectionJdbc.java
-------------------------

.. code-block::

    import java.sql.Connection;

    import java.sql.DriverManager;

    import java.sql.SQLException;

    import java.util.Scanner;



    public class ConnectionJdbc {

        private String userName;

        private String password;

        private String jdbcUrl;



        protected Connection currentconnection;



        public ConnectionJdbc() {

            this.userName = null;

            this.password = null;

            this.jdbcUrl = null;

        }

        public Connection getCurrentconnection() {

            return currentconnection;

        }



        public void setCurrentconnection(Connection currentconnection) {

            this.currentconnection = currentconnection;

        }



        public ConnectionJdbc(Connection connection) {

            this.currentconnection = connection;

        }



    //GETTERS AND SETTERS

        public String getUsername() {

            return userName;

        }



        public void setUsername(String username) {

            this.userName = username;

        }



        public String getPassword() {

            return password;

        }



        public void setPassword(String password) {

            this.password = password;

        }



        public String getJdbcurl() {

            return jdbcUrl;

        }



        public void setJdbcurl(String jdbcurl) {

            this.jdbcUrl = jdbcurl;

        }



    //Method to take input from user regarding url,passwd,and username

        public void enterConnectionDetails(){

            System.out.println("Enter jdbc url : ");

            Scanner url = new Scanner(System.in);

            jdbcUrl = url.next();



            System.out.println("Enter username : ");

            Scanner name = new Scanner(System.in);

            userName = name.next();



            System.out.println("Enter password : ");

            Scanner passwd = new Scanner(System.in);

            password = passwd.next();

        }

    //create connection

        public void makeConnection(){

            try {

                currentconnection = DriverManager.getConnection(jdbcUrl, userName, password);

                System.out.println("Successfully connected");

            } catch (SQLException e) {

                e.printStackTrace();

            }

        }



    }

2.5 CrudJdbcWithStatement.java
-------------------------------
.. code-block::

    import java.sql.*;



    public class CrudJdbcWithStatement extends ConnectionJdbc {



        private String createTableQuery,email,name;

        private Statement statement;

        private int id,age;





        public CrudJdbcWithStatement() {

            this.createTableQuery = null;

            this.email = null;

            this.name = null;

            this.id = 0;

            this.age = 0;

        }



        public String getCreateTableSQL() {

            return createTableQuery;

        }



        public void setCreateTableSQL(String createTableSQL) {

            this.createTableQuery = createTableSQL;

        }



        // Create table method

        public void createTable() {

            try {

                statement = currentconnection.createStatement();

                statement.executeUpdate(createTableQuery);



                System.out.println("Table Created Successfully");

            }

            catch (SQLException e) {

                System.out.println("Table Already exist");

            }

        }



        //Insert a row

        public void insertRow(){



            try {

                statement  = currentconnection.createStatement();

                String sql =    "INSERT INTO Users"

                        + "(id, name, age, email) " + "VALUES"

                        + "(1,'luna',23,'lhog@gmail.com')";

                statement.executeUpdate(sql);



                System.out.println("Rows inserted");

            } catch (SQLException e) {

                e.printStackTrace();

            }

        }



        //Read Table

        public void readTable() {

            try {

                System.out.println("Reading Table Data");

                statement = currentconnection.createStatement();

                ResultSet resultSet = statement.executeQuery("select * from Users");



                while (resultSet.next()) {



                    id = resultSet.getInt(1);

                    name = resultSet.getString(2);

                    age = resultSet.getInt(3);

                    email = resultSet.getString(4);



                    System.out.println("Id = " + String.valueOf(id) + " name = " + name + " age = " + String.valueOf(age) +

                            " email = " + email);

                }

            }

            catch (SQLException | NullPointerException e) {

                e.printStackTrace();

            }

        }



        //Delete a table

        public void deleteRow(int id) {

            try {

                statement = currentconnection.createStatement();



                String sql = "DELETE FROM Users" + " " + "WHERE id = " + String.valueOf(id);



                int result = statement.executeUpdate(sql);



                System.out.println("Rows deleted = " + result);

            }

            catch (SQLException e) {

                e.printStackTrace();

            }

        }



        //Update a row

        public void updateRow(int id, int updatedAge) {

            try {

                Statement statement = currentconnection.createStatement();



                int rows = statement.executeUpdate("Update Users" + " set age=" + updatedAge + " where id=" + id);



                System.out.println("Rows updated = " + rows);

            }

            catch (SQLException e) {

                e.printStackTrace();

            }

        }



    }

03. Mongodb
------------

3.1 Link
---------

 https://jalmeen@bitbucket.org/jalmeen/mongocrud.git

3.2 Dependency
---------------

.. code-block::

    <!-- https://mvnrepository.com/artifact/org.mongodb/mongodb-driver -->
    <dependency>
        <groupId>org.mongodb</groupId>
        <artifactId>mongodb-driver</artifactId>
        <version>3.4.2</version>
    </dependency>

3.3 Connection URI
--------------------

.. code-block::

    The format of the URI is:

    MongoClientURI uri  = new MongoClientURI("mongodb://user:pass@host:port/db"); 
            MongoClient client = new MongoClient(uri);
            MongoDatabase db = client.getDatabase(uri.getDatabase());


04. Minio Crud
---------------
https://jalmeen@bitbucket.org/jalmeen/minio.git

05 Mail Api
-------------

https://jalmeen@bitbucket.org/docdatreon/javamailapi.git

06 Sshj
--------
work flow...

https://jalmeen@bitbucket.org/jalmeen/sshjcode.git

07 Thumbnailator
------------------

Codeflow...

https://jalmeen@bitbucket.org/jalmeen/thumbnailator.git

08 Jsoup
---------
09 Xml ParsingBook
------------------
10. Json ParsingBook
---------------------
11. Csv ParsingBook
---------------------
12. Jndi CRUDBook
-------------------

13. Pdf CrudBook
---------------------

