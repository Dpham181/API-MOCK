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

### Json file create for requesting in post method: 

* Create json-file: follow, tweet, and user (files located share folder called follow.json, tweet.json, and user.json)

### SH files (located bin folder): 

1. init.sh (exeute ddl file )
2. PostFollow.sh (post a new follow )
3. PostTweet.sh (post a new tweet)
4. PostUser.sh (post a new user) 


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

5. /bin/init.sh (initial the database for sqlite)

6. foreman start ( runinng all the services)

7. open new terminal

8. In the new terminal: 
  * For posting using sh, we need to locate to root folder then typing the following command: 
      -  ./bin/PostUser.sh ./share/user.json  (for create new user)

      -  ./bin/PostFollow.sh   ./share/follow.json (for create new follow)
      -  ./bin/PostTweet.sh ./share/tweet.json (for posting a new tweet) 

  * For execution direct with commnad line, so you just need to copy/paste or typing:
    -   http --verbose http://localhost:5100/users/test1/auth/123 (authenticate a user)

    -   http --verbose DELETE http://localhost:5100/users/test2/remove_follower/test3
 (user one remove follower user 3)
 
    -   http --verbose http://localhost:5200/users/test2/Posts (get user timelines )
    -   http --verbose http://localhost:5200/Posts (get public timelines)
    -   http --verbose http://localhost:5200/users/test2/Following/Posts (get home timelines)
 
 

