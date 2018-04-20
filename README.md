# CRUD
Restful web-service library written in C++11  based on boost.ASIO and CRUD handlers

### REST handler with regex

```C++
    using regex_restful_dispatcher_t =  http::crud::crud_dispatcher<http::server::request, http::server::reply>;
    regex_restful_dispatcher_t regex_handler(".") ; //root is irrelavant for REST only used for web-server
    regex_handler.crud_match(boost::regex("/venue_handler/(\w+)") )
                 .post([](http::server::reply & r, const http::crud::crud_match<boost::cmatch> & match) {
                    r << "{}" << http::server::reply::flush("json") ;
                    std::cout << "POST group_1_match=[ << match[1] << "], request_data=" << match.data << std::endl;
                 });
```

### simple REST handler

```C++
   // SIMPLE NO REGEX MATCH FOR POST "/venue_handler/RTB"
    using simple_restful_dispatcher_t = http::crud::crud_dispatcher<http::server::request, http::server::reply, std::string, std::string>;
    simple_restful_dispatcher_t simple_handler(".") ; //root is irrelavant for REST only used for web-server
    simple_handler.crud_match(std::string("/venue_handler/RTB") )
                  .post([](http::server::reply & r, const http::crud::crud_match<std::string> & match) {
                     r << "{}" << http::server::reply::flush("json") ;
                     std::cout << "POST request_data=" << match.data << std::endl;
                   });
```
### All in one go
```C++
    // CREAT/READ/UPDATE/DELETE "/venue_handler/XEMDP/123"
    handler.crud_match(boost::regex("/venue_handler/(\\w+)/(\\d+)") )
           .put([](http::server::reply & r, const http::crud::crud_match<boost::cmatch> & match)
              std::cout << "CREATE request=" << match[0] << "/" << match[1] << std::endl;
              r = http::server::reply::stock_reply(http::server::reply::no_content);
           })
           .get([](http::server::reply & r, const http::crud::crud_match<boost::cmatch> & match) {
              r << "name: " << match[1] << ", instance number: " << match[2]
                << http::server::reply::flush("text") ;
              std::cout << "READ request=" << match[0] << std::endl;
           })
           .post([](http::server::reply & r, const http::crud::crud_match<boost::cmatch>  & match) {
              r << "name: " << match[1] << ", instance number: " << match[2]
                << http::server::reply::flush("text") ;
              std::cout << "UPDATE request=" << match[0] << std::endl;
              std::cout << "UPDATE request_data=" << match.data << std::endl;
           })
           .del([](http::server::reply & r, const http::crud::crud_match<boost::cmatch> & match)
              std::cout << "DELETE request=" << match[0] << "/" << match[1] << std::endl;
              r = http::server::reply::stock_reply(http::server::reply::no_content);
           }) ;
```

### Setting up connection types

#### For keep-alive persistent connections specifiy second template argument with presistent type for connection
```C++
http::server::server<simple_restful_dispatcher_t, http::server::persistent_connection> server{host,port,handler};
```

#### By default server is using non-persistent connection from the library 
```C++
http::server::server<simple_restful_dispatcher_t> server{host,port,handler};
```
