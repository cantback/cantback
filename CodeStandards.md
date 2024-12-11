
[toc](List)
## Overall
- This Java code writing specification is based on Alibaba's "Alibaba Java Development Manual Ultimate Edition" code specification, and some specifications may be adapted to our team's coding changes.  For areas not covered in this article, please refer to the Alibaba Java Standard Code Specification. 

## Programming protocol 
### Code Style 
1.1 All names in the code must not start or end with an underscore or dollar sign.  Counterexample:  Name/__name/$Object/name_/name $/Object$ 
1.2 All names in the code are prohibited from using Pinyin or Chinese, and English should be used correctly. 
1.3 Naming conventions for classes, methods, and variables. 
- 1.3.1 Class namesThe class name should use the UpperCamelCase naming convention, with the first letter capitalized, and the naming should be descriptive and reflect the functionality of the class.  For example: Student Manager, DatabasMananger. 
- 1.3.2 Method Name 
   The method name should use the lowerCamelCase naming convention, with the first letter in lowercase, and the verb should clearly indicate the function that the method can achieve.  For example: calculateTotalPrice(), getUserInfo(). 
- 1.3.3 Variable Names 
  Variable names should use the lowerCamelCase naming convention and avoid using single letter variable names (unless in a loop).  Reflect the actual meaning of variables such as totaCost and useNumber. 
1.4 Class name suffix 
- Class names often use different suffixes to express additional meanings, such as:Service 	Indicates that this class is a service class that includes methods for providing the same business services to other classes 	PaymentOrderService
1.5 Constant names are all capitalized, separated by underscores between words, striving for complete and clear semantic expression, without any bias towards word length. 
1.6 It is not allowed to maintain one constant over another. Each constant should be declared by function for maintenance purposes, 
1.7 Package and file structure 
- Package Name: Package names should be written in lowercase letters, avoiding the use of special symbols, and divided according to functional modules.  For example: com. university. projectname. control 
- File structure: The file structure of the project should be clear and divided by functional modules, such as src/main/java/com/university/projectname/controller/ 
## Code format 
2.1 Indentation 
- Use 4 spaces for indentation, do not use tabs. 
2.2	Spaces and line breaks 
- The statement block {} that controls the structure should be included even if there is only one line. 
- There should be a blank line between each method and class to increase the readability of the code. 
2.3	Adding annotations 
- Class comments: Each class should have a comment at the beginning, briefly explaining the functionality, purpose, and developer information of the class. 
- Method comments: Each method should have comments, especially public methods, explaining its functionality, parameters, return values, and exception situations. 
- Logical comments: Comments should be added before complex logical code to help other developers understand the design and implementation of the code. 
Example: 


```
/** 
 * calculate the sum of students grade 
 * @param studentList 
 * @return sumOfGrade 
 */ 
public double calculateTotal(List<Student> studentList) { 
    double total = 0.0; 
    for (Student student : studentList) { 
        total += student.getScore(); 
    } 
    return total; 
} 



```


2.4 Annotation Standards 
2.4.1 Annotations vs. Code 
1. Annotations should be concise but not excessive or misleading 
2. Naming conveys meaning, with clear structure and clear responsibilities for classes and methods, often requiring minimal or no annotations to make it easy for people to understand;  On the contrary, the code is chaotic, and no amount of comments can make up for it.  So, we should first focus on the code itself. 
3. Comments that cannot express the meaning of the code correctly will only damage the readability of the code. 
4. Overly detailed comments, comments added to obvious code, and verbose comments are better left blank. 
5. Comments should be synchronized with the code, as excessive comments can become a burden on development 
6. Annotations are not used to manage code versions. If there is any code that needs to be removed, it can be deleted directly. SVN will record it, so do not comment it out. Otherwise, no one will know whether the commented out code should be deleted in the future. 
2.4.2Java Doc 

- Annotations indicating the meaning and usage of classes, fields, methods, etc. should be written in the format of Javadoc.  Java Doc is designed for class users, mainly introducing information such as what it is and how to use it.  Any user of a class needs to know and use Java Doc to write it.  Non Java Doc comments are often read by code maintainers, emphasizing why they are written this way, how to modify them, and what issues to pay attention to.  As follows: 

```

/** 
* This is a class comment 
*/ 
public class TestClass { 

    /** 

    * This is a field comment 

    */ 

    public String name; 

    /** 

    * This is a method comment 

    */ 

    public void call() { 

    } 
}

```
2.5  In-line comments are written with // at the end of the line
2.6 Use log instead of System. out. println(). 
- log to set levels and control where output is sent, making it easy to distinguish where it is printed in the code, while System. out. print does not. Moreover, the speed of System. out. print is very slow.  So, unless it's intentional, logs should be used.  Replace System. out. print with log at least before submitting to svn 

2.7  Reduce the level of code nesting. When the level of code nesting reaches more than 3 layers, it will be difficult for most people to understand. 

### Unit testing
3.1 Write unit tests using JUnit or other testing frameworks.  Each module/method should have corresponding test code to ensure functional correctness. 

3.2. Following the principle of "test first", which means writing corresponding test cases before writing functional code. 
Example: 
```
@Test 
public void testCalculateTotal() { 
    List<Student> students = Arrays.asList(new Student("John", 85), new Student("Alice", 90)); 
    double total = calculateTotal(students); 
    assertEquals(175.0, total, 0.001); 
} 
```

### Version control and collaboration 
4.1 Using Git for version control 
- All team members should use Git for code management and regularly submit code. 
Each time you submit, the submitted information should be clear and concise, describing the main functions and repair content of this submission.  For example, 'fixing bugs in student grade calculation methods' instead of' fixing bugs'. 
- Create feature branches during development and merge them into the main branch (such as master or main) after completion. 
4.2 Code review 
 - When each team member submits code, they should request other members to conduct a code review.  Code review mainly checks the quality of code, compliance with specifications, and correctness of functionality. 
4.3 Documents and Annotations 
-  During the development process, keep the project documentation updated to ensure that team members are aware of project progress, module allocation, interface design, and more. 
-  For each module/class, it is recommended to write a brief explanatory document that explains the functionality, design ideas, and development considerations of the module. 
### Programming Tools and Environment 
5.1 development tool 
 -  Use IntelliJ IDEA as the primary development tool. 
 - Configure the IDE to conform to the coding style of the project, enabling features such as code formatting, syntax checking, and auto completion. 
5.2 Building Tools 
-  Use Maven or Gradle for project construction and dependency management. 
-  Ensure that team members use the same build tools to avoid version conflicts. 
5.3 Dependency Management 
- Try to use public Maven repositories for project dependencies, avoid using local repositories, and ensure consistency of dependencies between teams. 
- Regularly update dependent versions to avoid using outdated libraries.

### MySQL database
6.1 Table Creation Conventions
- Fields that represent the concept of "yes" or "no" must be named using the format is_xxx, and the data type should be unsigned tinyint (1 for yes, 0 for no).
- Table names and field names must use lowercase letters or numbers. It is prohibited to start with a number or use numbers between two underscores. The modification cost of database field names is high, so lowercase letters and underscores should be used, with underscores separating words.
- Table names and field names must not use reserved keywords (e.g., type, order, status).
- Table names should not use plural nouns.
- Table aliases must be lowercase, and table aliases must be set with the prefix as.
- Field naming should uniformly use the underscore naming convention; camel case naming is prohibited.
- Table names, field names, and table aliases must not use MySQL reserved keywords (e.g., desc, range, match, delayed).
- Primary key index names should be pk_field_name; unique index names should be uk_field_name; non-unique index names should be idx_field_name.
- Decimal data types should be used for floating-point numbers, and float and double should not be used.
- If the stored string lengths are nearly identical, use char instead of varchar.

6.2 Indexing Conventions
- Fields that have unique business characteristics, even if they are a combination of multiple fields, should have a unique index.
- Joins involving more than three tables are prohibited. The fields involved in a join must have the same data type. When performing multi-table join queries, ensure that the fields being joined have indexes.
- Index files must be stored on a separate disk from the data files. The indexes should be placed in separate .idb files and not in the same filegroup as the data files.
- Index names must begin with idx_.
- The number of indexes on a single table should not exceed five.
- InnoDB tables must have a primary key index.
- InnoDB tables must have an auto-increment primary key, and the primary key should be named id.
- The primary key index type must be BTREE.

### Java Development Security Conventions
7.1 Input Validation and Sanitization

- Always validate and sanitize user inputs to prevent injection attacks such as SQL injection, XSS (Cross-Site Scripting), and command injection.
- Use prepared statements (e.g., PreparedStatement for SQL queries) to protect against SQL injection.
- Sanitize HTML and JavaScript content using libraries such as OWASP Java HTML Sanitizer or equivalent to prevent XSS attacks.

7.2 Secure Password Handling

- Always store passwords securely using modern hashing algorithms such as bcrypt, PBKDF2, or Argon2. Do not store plaintext passwords.
- Avoid using weak hashing algorithms like MD5 or SHA1.
- Use strong password policies, such as requiring a mix of uppercase, lowercase, numbers, and special characters.
- Implement account lockout or delay mechanisms after a certain number of failed login attempts to prevent brute-force attacks.

7.3 Secure Communication

- Use HTTPS (SSL/TLS) for secure communication between clients and servers.
- Ensure that the SSL/TLS certificates are up to date and properly configured.
- Avoid using weak encryption protocols (e.g., SSL 2.0, SSL 3.0, or early versions of TLS).

7.4 Access Control and Authentication

- Implement the Principle of Least Privilege: Users should only have the minimum access needed to perform their tasks.
- Use strong authentication mechanisms, such as two-factor authentication (2FA), where feasible.
- Protect sensitive endpoints with proper role-based access controls (RBAC) or attribute-based access controls (ABAC).
- Always use OAuth2 or OpenID Connect for third-party authentication when appropriate.
