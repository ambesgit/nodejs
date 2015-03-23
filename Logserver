/*
this server can access database and retrive questions and answers and send to the client connected 
then based on the answer of the question, the server will respond correct or wrong based
beside this the server will log meta data of any client connected to it
based on the meta data and number of questions answered , analysis of the data may be done
then based on the result decission may be made to improve quality of education in schools
But this server is far from the idea, it needs much more thinking and code accordingly but the idea is cool
*/



//load the native net module to memory and retun me the pointer to this object so i will use to create sockets
var app=require("net");
//load the native file system and return me the pointer to this object so i will manipulate files 
var fs=require("fs");
//this will store all the sockets created by the server for each client connected to it
var clients=[];
//this will hold the number of visits the server gets since it becomes online
var connectedClients=0;
//the create method will return a socket that can be read and write to it
var Logserver=app.createServer();
    /* when a client connected to the logserver the connection event will emited by the logserver
    # as you know, if the connection is establish, the server will create another socket
    #this new socket created by the server will be used only by the connected client to 
    #this new socket and this new socket can be accessed using callback function
    #then access meta data of the connected client
    */
    Logserver.on("connection",function(socket){
        //every time a client is connected the connectedClients will be updated
        connectedClients+=1;
        //set the encoding type to the socket explicitly
        socket.setEncoding("utf8");
        //the address method returns address object of the server
        var sd=socket.address();
        //the address object will be changed to string using the JSON stringify method inorder to be written to file
        var st=JSON.stringify(sd);
        //the fil variable will hold a reference to the path of the file that stores the client meta data log information
        var fil="../clientLog.txt";
        // the current clients meta data information will be written to the specified file
        fs.appendFile(fil,st+"\n")
        //Here the clients remote address and port number will be accessed from the socket and save to the file
        fs.appendFile(fil,socket.remoteAddress+" "+"port"+":"+socket.remotePort+"\n");
        //this will put a time stamp that the client is connected to the server
        fs.appendFile(fil,new Date+"\n");
        //at the time that this client is connected, how many connections were serveed by the server Pluse you
        fs.appendFile(fil,"number of connection"+":"+connectedClients+"\n");
        //push all the sockets created by the server to the array 
        //this will help to send messages from the server to the currently connected clients        
        
        clients.push(socket);
      
        //this server will ask questions to the client(let say student) 
        socket.write("Question .1:"+"\n"+" simplify x(x+y)=2x+10y"); 
        var answer="the answer to the question";
        
        //listen to the data event and grap the message comming from the client
        
        socket.on("data",function(data){
            if(data===answer){
              /* if you want you may keep record of the number of correct answers of a particuler student and
                you can built on top of this to create a cool app for computition
                behind the seen you can do analysis of the meta data and come up with different statisctics based on 
                country, school, subject, and so on
                based on the result of the analysis decission may be made 
            */
            
            socket.write("correct");            
            }
            else{
            socket.write("wrong");
            
            }     
    
    });
        
     // listen to the end event then remove the client from the clients array becaause you don't stored a dead socket in the array   
    socket.on("end",function(){

    var index=clients.indexOf(socket);
        
        clients.splice(i,1);        
    
    });
      
    
});
/*the server starts listening on port 8080 and the time and data is recorder 
this will help to know for how long the server is online and if needed, maintenance may be required 
so another machine has to take the role of this server(hardware), if this machine is member of a cluster of machines
also the date is written to the log file and to the screen
*/
Logserver.listen(8080,function(){console.log("server is runing");
            console.log(new Date)                 
            fs.appendFile("../clientLog.txt",new Date+"\n");                
            });
