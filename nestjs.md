# Nest js

## Relation And Populate

##### In node js

staff_id:{
type:mongoose.Schema.TYpes.ObjectId,
ref:"Staff"
}

().populate("staff_id)

#### Path and Math

staff_id:[{
type:mongoose.Schema.TYpes.ObjectId,
ref:"Staff"
}}

.populate({
path:"staf_id",
match:{
name:"Sachin",
email:"sachin@gmail.com"
}
})

--> use like

```js
.populate({
path:"staf_id",
match:{
email:{
$regex:
}
}
})

{
$eq:""
}


{
$ne:""
}
```

#### Sorting & Limit

```js
.populate({
path:"staf_id",
select:"-_id name",
options:{
    sort:{ name:"-1"}
    limit:2
}
})
```

#### Nested Pupulation

auth -> post -> comments

```js
find({naem:"sachin}).populate({
path:"Post",
populate:{
path:"comments
populate:{
path:"comments
}
}
})
```

## Cookie Based authentication with passport jwt

> > npm i --save cookie-parser passport possport-jwt @nestjs/passport

> > npm i --save-dev @types/passport-jwt @types/cookie-parser

```js
in main.ts
- import * as cookieParser from "cookie-parser"
  app.use(cookieParser())
```

- create auth module

```js
jwtstrategy.ts

import {ExtractJwt,Strategy} from "passport-jwt";
import {PassportStrategy} from "@nestjs/passport";
import {Request as RequestType } from "express";
import { Injectable } from "@nestjs/common";


export const JwtSecretTMP="secretKey"
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy){
    constructor(){
        super({
            jwtFromRequest:ExtractJwt.fromExtractors([jwtStrategy.extractJWT,ExtractJwt.fromAuthHeaderAsBearerToken()]),
            ignoreExpiration:false,
            secretOrKey:JwtSecretTMP
        })
    }
// jwtStrategy.extractJWT this will call the below function if this function does  not execist it use next things ExtractJwt.fromAuthHeaderAsBearerToken() get access from header
private static extractJwt(req:RequestType):string|null{
    if(req.cookies&&"user_token" in req.cookies && req.cookies.user_token.length>0){

        return req.cookies.user.token;
    }
    return null
}

async validate(payload:any){
    return {user:payload.id};
}

}

```

npm i --save @nestjs/jwt

```js
in auth module.ts
import {JwtModule} from "@nestjs/jwt";
import {PassportModule} from "@nestjs/passport"
imports:[PassportMOdule.register({defaultStrategy:"jwt",session:false}),
JwtModule.register({secret:JwtSecretTMP,signOptionIN:"1h"})

]
providers:[JwtStrategy],
controller:[AuthController]

```

```js
guard;

@Injectable()
export class JwtGuard extends AuthGuard("jwt") {}
```

```js
@UseGuard(JwtGuard)
@COntroller()



```

```js
// auth controller
import {JwtService} from "@nestjs/jwt"
@COntroller("auth")
export class AuthController{

    constructor(private jwtService:JwtService){}

    @Get()
    async login(@Res({passthrough:true}  res) ){
        const payload={usernam:"john",id:1};
        // return {
        //     access_token:this.jwtService.sign(payload)
        // }
        // or

        res.cookie("user_token",this.jwtService.sign(payload),{
            expires:new Date(Date.now()+3600000),
        });

           res.cookie("user_token",this.jwtService.sign(payload),{
            secure:true,
            httpOnly:true,
            expires:new Date(Date.now()+3600000),
        });
        return {}
    }

    @Get("lagout")
    async lagout(@Res({passthrough:true}) res)
    res.cookie("user_token","",{express:new Date(Date.now())});
    return {}
}

```

in nest js

![alt text](./assests/cookies.png)

![alt text](./assests/cokkie_server.png)

## AUthentication and authorization using JWT in nestjs

### using passport

npm i --save @nestjs/passport passport-local
npm i --save-dev @types/passport-local

--> user.module.ts

--> auth.module.ts
```js
imports:[UserModel]
providers:[PassportLocalStrategy]
```
--> passport.local.strategy.ts

```js
import {PassportStrategy} from "@nestjs/passport";
import {Strategy} from "passport-local";

@Injectable()
export class PassportLocalStrategy extends PassportStrategy(Strategy){

   constructor(private readonly userService:UserService){
    super();
   }

   validate(username:string,password:string){
const user=this.userService.getUserBYName(username);
   if(user==undefined)
       throw new UnothorisedExecption("message")
   }
   return username;
}
```

@UseGuard(AuthGuard("local"))

--> guard

```js




```

all api must have  username and passowrd in body

### using jwt

npm i @nestjs/jwt @nestjs/passport passport passport-jwt passport-local
@types/passport-jwt
@types/passport-local

--> in auth.module.ts
import {PassportModule} from "@nestjs/passport";
import {JwtModule} from "@nestjs/jwt";

imports:[
    PasssportModule,
    JwtModule.register({
        secret:"abc",
        signOptions:[expiresIn:"1h"]
    })
],
providers:[LocalStrategy,JwtStrategy]

--> in authService.ts
```js
import { JwtService } from '@nestjs/jwt';
constructor(jwtService:JwtService){}

return this.jwtService.sign({user:"asd@12"})
```
--> in auth.controller.ts

--> local.strategy.ts
```js
import {PassportStrategy } from @nestjs/passport";
import {Strategy} from "passport-local";
import {AuthService} from "@nestjs/common";

@Injectable
export class LocalStrategy extends PassportStrategy(Strategy){
    constructor(private authService:authService){
        super();
    }

    validate(username:string){
     const user=this.authService.validateUser(username)

     if(!user)
     throw new UnauthorizationException();

     return user;
    }
}
```


```js
import {AuthGuard} from "@nestjs/passport"
@UseGuards(LocalGuard())
```

--> guard
```js
guard.ts

import {ExecutionCOntext,Injectable} from "@nestjs/common";
import {AuthGuard} from "@nestjs/common";
import {Observable} from "rxjs"

export class LocalGuard extends AUthGuard("local"){
    canActivate(context:ExecutionContext):boolean | Promise<boolean> | Observable<boolean>{}

    return super.canActivate()
}
```

```js
import {PassportStrategy } from @nestjs/passport";
import {Strategy} from "passport-jwt";
import {AuthService} from "@nestjs/common";

@Injectable()
export class JwtStrategy extends PassportStrategy(strategy){
    constructor(){
        super({
            jwtFromRequest:ExtractJwt.fromAuthHeaderAsBearerToken(),
            ignoreExpiration:false,
            secretOrKey:"0asdas",

        });
    }

    validate(payload:any){
     const user=this.authService.validateUser(payload.userId)

     if(!user)
     throw new UnauthorizationException();

     return payload;
    }  



}

```
--> jwt.guard.ts
```js
import {ExecutionCOntext,Injectable} from "@nestjs/common";
import {AuthGuard} from "@nestjs/common";
import {Observable} from "rxjs"
export class LOcalGuard extends AUthGuard("jwt"){
    canActivate(context:ExecutionContext):boolean | Promise<boolean> | Observable<boolean>{}

    return super.canActivate()
}


```

@UseGuard(JwtAuthGuard)

```js
---> app.module.ts

 providers: [AppService, {
    provide: APP_GUARD,
    useClass: JwtGuard,
  },],
```

--> jwtGuard.ts

```js
import { ExecutionContext, Injectable ,} from '@nestjs/common';
import { Reflector } from '@nestjs/core';
import { AuthGuard } from '@nestjs/passport';
import { Observable } from 'rxjs';
import { IS_PUBLIC_KEY } from '../decorator/public.decorator';

@Injectable()
export class JwtGuard extends AuthGuard('jwt') {
    constructor(private reflector: Reflector) {
        super();
    }
    canActivate(context: ExecutionContext): boolean | Promise<boolean> | Observable<boolean> {
        const isPublic = this.reflector.get<boolean>(IS_PUBLIC_KEY, context.getHandler());
        if (isPublic) {
          return true;
        }
        return super.canActivate(context);
    }
}
```

export class AppModule implements OnModuleInit {
  async onModuleInit() {
    console.log(process.env.MONGO_URI)
  }
}




### Class Validator and class Transformer