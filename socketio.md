                              Socket io                                 

websocket / http /ftp/smtp → communication protocol


Before websocket polling were use but that is over kill ( ask server again and again )

io (server)  , socket (client)
emit → send message to all active socket , 
on → trigger event  , 
broadcast → send to all another than who trigger event , 
to → for personal chat  , 
join → to join in a room or create a group

npm init -y

—---------  Client —--------

Npm i socket.io-client

import {io} from “socket.io-client”

const socket=io(“http://localhost:3000”);  // if don’t pass any it will look into same port
// this will rerender on every render to resolve this use useMemo
const socket =useMemo(()=>io(“http://localhost:3000”),[])


useEffect(() => { 
socket.on("connect", () => { console.log("connected", socket.id);
 socket.on("welcome", (message) => { console.log(message); }); });

 // Cleanup to prevent memory leaks
 return () => { socket.off("connect"); 
socket.off("welcome"); 
socket.disconnect()
} }, []);


function sendMessage(){
socket.emit(“message”,”message data”)
}
 —-------- Server  —------- 

Npm i socket.io

Import express from “express”
Const port =3000;
const app=express();

const {createServer} from “http”;
const {Server} from “socket.io”
Import cors from “cors”


const server=createServer(app)
const io=new Server(server,{
cors:{origin:[“http:localhost:5173”],
method:[“GET”,”POST”],
credentials:true}})


// this will work as a middleware
io.use((socket,next)=>{
next()
})

io.on(“connection”,(socket)=>{
console.log(“user connected”,socket.id)

 socket.on('disconnect', () => { console.log('user disconnected'); });
socket.emit(“welcome”,”welcome to the server”)
socket.broadcast.emit(“welcome”,”welcome to the server”)


io.to(“rom_id”).emit(“receive-message”,message)
       —------ or —---------
socket.to(“rom_id”).emit(“receive-message”,message)


socket.on(“join-room”,(room)=>{

socket.join(room_name)
})

socket.on(“message”,(data)=>{
console.log(data)
}
})

app.use(cors({
origin:[“http:localhost:5173”],
method:[“GET”,”POST”],
credentials:true
}))
server.listen(port,()=>{
console.log(“server started a at port”
})


                                 Socket io Nest js  


npm i @nestjs/websockets @nestjs/platform-socket.io
nest g module chat

chat-gateway.ts

import { SubscribeMessage, WebSocketGateway, OnGatewayInit, OnGatewayConnection, OnGatewayDisconnect } from '@nestjs/websockets';
import { Logger } from '@nestjs/common';
import { Socket, Server } from 'socket.io';

@WebSocketGateway()
—------------ or —--------------
@WebSocketGateway(3002,{cors:{origin:[“http:localhost:5173”],
method:[“GET”,”POST”],
credentials:true}})
export class ChatGateway implements OnGatewayInit, OnGatewayConnection, OnGatewayDisconnect{
private logger: Logger = new Logger('ChatGateway');

@WebSocketServer() server: Server;

@SubscribeMessage('message') 
handleMessage(client: Socket,@MessageBody() message:any): void {
console.log(message)

this.server.emit(“reply”,”this is the message”)

client.emit(“reply”,”this is a reply)
 }

afterInit(server: Server) { 
this.logger.log('Init');
 } 

handleDisconnect(client: Socket) 
{ this.logger.log(`Client disconnected: ${client.id}`); } 

handleConnection(client: Socket, ...args: any[]) { 
this.logger.log(`Client connected: ${client.id}`); }



}

providers:[chatGateway]

Postman 
socket.io → Url → 


Import another services and perform actions 

// src/app.module.ts
import { Module } from '@nestjs/common';
import { MongoModule } from './mongo/mongo.module';
import { UserModule } from './user/user.module';  // Import the UserModule
import { AppGateway } from './app.gateway';

@Module({
  imports: [MongoModule, UserModule],  // Include UserModule here
  providers: [AppGateway],
})
export class AppModule {}

constructor(@Inject(UserService) private readonly userService: UserService) {}


                                         acces Token with socket.io     

io(SOCKET_URL, {
 transports: ['websocket'], // Optional: to enforce WebSocket transport 
query: { token }, // Sending token as a query parameter

 // Alternatively, you could use headers if your server supports it 
//transportOptions: { 
// polling: {
 // extraHeaders: { 
// Authorization: `Bearer ${token}`
 // } 
// } 
// } });  

import { io } from 'socket.io-client';

const socket = io(SOCKET_URL, { 
  transports: ['websocket'], // Use WebSocket transport
  extraHeaders: { 
    Authorization: `Bearer your_access_token` // Custom headers
  },
  query: { 
    param1: 'value1', // Add your query parameters here
    param2: 'value2'
  }
});



const socket = io(SOCKET_URL, { 
transports: ['websocket'],
transportOptions:{
 websocket: { 
extraHeaders: { 
Authorization: `Bearer your_access_token` 
} } } });

// Alternatively, you could use headers if your server supports it 
//transportOptions: { 
// polling: {
 // extraHeaders: { 
// Authorization: `Bearer ${token}`
 // } 
// } 
// } });    i want to use this we need to add 
transports: ['websocket', 'polling']    
 

                                  Use of query 
async handleConnection(client: any, ...args: any[]) { const token = client.handshake.query.token;

                                 Use of Header

const token = client.handshake.headers['authorization'];


 Callback in socket io 
Client  
socket.emit("update item", "1", { name: "updated" }, (response) => {
 console.log(response.status); // ok
});

Server          
io.on("connection", (socket) => {
 socket.on("update item", (arg1, arg2, callback) => {
   console.log(arg1); // 1
   console.log(arg2); // { name: "updated" }
   callback({
     status: "ok"
   });
 });
});

Can  add  timeout if the response does not came
socket.timeout(5000).emit("my-event", (err) => {
 if (err) {
   // the other side did not acknowledge the event in the given delay
 }
});

socket.timeout(5000).emit("my-event", (err, response) => {
 if (err) {
   // the other side did not acknowledge the event in the given delay
 } else {
   console.log(response);
 }
});

Volatile events


io.on("connection", (socket) => {
 console.log("connect");
 socket.on("ping", (count) => {
   console.log(count);
 });
});
let count = 0;
setInterval(() => {
 socket.volatile.emit("ping", ++count);
}, 1000);
Listening to events
socket.once(eventName, listener)​
Adds a one-time listener function for the event named eventName
socket.once("details", (...args) => {
 // ...
});


socket.off(eventName, listener)​
const listener = (...args) => {
 console.log(args);
}
// and then later...
socket.off("details", listener);

socket.removeAllListeners([eventName])​
Removes all listeners, or those of the specified eventName.
// for a specific event
socket.removeAllListeners("details");
// for all events
socket.removeAllListeners();

socket.onAny(listener)​
Adds a listener that will be fired when any event is emitted.
socket.onAny((eventName, ...args) => {
 // ...
});

socket.onAnyOutgoing(() => {
 // triggered when the event is sent
});
socket.offAny(listener);

// or all listeners
socket.offAny();

socket.offAnyOutgoing([listener])​
Removes the previously registered listener. If no listener is provided, all catch-all listeners are removed.
const listener = (eventName, ...args) => {
 console.log(eventName, args);
}

socket.onAnyOutgoing(listener);

// remove a single listener
socket.offAnyOutgoing(listener);

// remove all listeners
socket.offAnyOutgoing();

Broadcasting events


io.to("room123").timeout(5000).emit("hello", "world", (err, responses) => {
 // ...
});
from a specific socket
socket.broadcast.timeout(5000).emit("hello", "world", (err, responses) => {
 // ...
});

