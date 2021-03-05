# CPSC 449 - Web Back-End Engineering 
## Project 2 
## Spring 2021 due March 12 (Section 02)


# We plan to build a microblogging service similar to Twitter
#### Messages are aggregated into timelines. There are three different timelines:
    1.Each user has a user timeline consisting of the posts that they have made.
    2.Each user has a home timeline consisting of recent posts by all users that this user follows.
    3.There is a public timeline consisting of all posts from all users.
    4.Timelines are organized in reverse chronological order. When timelines are retrieved through the web service, they should be limited to 25.

# Project design 

### Relational Database Creation:

* Create three Enity: Users, Follow, and Post (DDL file located share folder called project2.sql) with including the mock datas. 


### SH files (located bin folder): 

1. init.sh (exe ddl file )


### services file .py (located in root folder)

1. apy.py ( intital app config and 2 methods of query the database)
2. TimelinesService.py (Timelines service) 
3. UsersService.py (Users service)

### config files
1. Procfile (located in root folder): use to runing all the above services.
2. project2.db (located in var folder): this is file that holding database after executing the ddl file. 
3. app.ini and logging.ini (located in etc folder): use to inital the bottle app and connecting database. 
### URI host:
1.  http://localhost:5000/ (api initial)
2.  http://localhost:5100/ (Users service)
3.  http://localhost:5200/ (Timelines service)
# Project exe commandline:

1. sudo apt update

2. sudo apt install --yes python3-pip ruby-foreman httpie sqlite3

3. python3 -m pip install bottle bottle-sqlite

4. cd Danh_sProject2

5. ./bin/init.sh (initial the database for sqlite note if it required permission then use chmod +x init.sh) 

6. foreman start ( runinng all the services)

7. open new terminal

8. In the new termail. Now we can use Httpie command in-order to execute all the fucntions requirement

      #### Create new user 
      ##### http --verbose POST localhost:5100/users/ {json data}
      ###### http --verbose POST localhost:5100/users/ UserName="test4" PassWord="123" Email="test4@gmail.com"


      #### Authenticate user 
      ##### http --verbose POST http://localhost:5100/users/{username}/auth {json data}
      ###### http --verbose POST  http://localhost:5100/users/test4/auth  PassWord="123"


	
      #### User follow 
      ##### http --verbose POST http://localhost:5100/users/{username}/add_follow/ {json data}
      ###### http --verbose POST http://localhost:5100/users/test4/add_follow/ FOLLOWER="test4" FOLLOWING="test1"
       
      #### User follow 
      ##### http --verbose DELETE http://localhost:5100/users/{username}/remove_follower/ {json data}
      ###### http --verbose DELETE http://localhost:5100/users/test4/remove_follower/ FOLLOWING=test1
       
      #### User timelines (desc limit 25 )
      ##### http --verbose http://localhost:5200/users/{username}/Posts {json data}
      ###### http --verbose http://localhost:5200/users/test1/Posts
       
      #### Public timelines  (desc limit 25)
      ##### http --verbose http://localhost:5200/Posts 
      ###### http --verbose http://localhost:5200/Posts
       
       
      #### Home timelines   (desc limit 25)
      ##### http --verbose http://localhost:5200/users/{username}/Following/Posts
      ###### http --verbose http://localhost:5200/users/test1/Following/Posts
       
       
      #### POST Tweet 
      ##### http --verbose POST http://localhost:5200/users/{username}/Posts/ {json data}
      ###### http --verbose POST http://localhost:5200/users/test1/Posts/ Text=test
       
