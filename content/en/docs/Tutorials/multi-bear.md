---
title: "Validation"

weight: 4
description: >
 Here we talk about about validation of user's input.
---

### IT IS VERY IMPORTANT
---
**Most of the attackers exploite the server by input data.**

---

### DTOs

As in any other programming frameworks, Nest provides us with built in libraries.
In our template project, in each folders (users, posts e.t.c) you can see dto folders.
Here we define the form of data that any sevice function takes as argument. And here,
we also validate that data.

### Example 1
---
*Go to posts/dto/CreatePostDto*

 ```js
    export class CreatePostDto {
    @ApiProperty({example: 'Searching for metal supplier for our company', description: 'Title of post, should be between 5 and 60 symbols'})
    @IsString({message: 'Should be a string'})
    @Length(5, 60, {message: 'The length of post title should be between 5 and 60'})
    
    readonly title: string;
    @ApiProperty({example: 'Searching for metal supplier for our company and much more...', description: 'The content part of post should consist of 0 - 700 sybmols'})
    @IsString({message: 'Should be a string'})
    @Length(5, 500, {message: 'The length of post title should be between 5 and 500'})
    readonly content: string;
  
    @ApiProperty({example: '6', description: 'The id of user, whose post it is'})
    readonly userId: number;
}
``` 

As you can see above, we validate each input variable. For example, we make sure that title of the post is string (no SQL injection) and the length of the title is limited.

---

### Example 2

---

*Go to users/dto/createUserDto*

 ```js
   export class CreateUserDto {
    @ApiProperty({example: 'user@mail.ru', description: 'mail'})
    @IsString({message: 'Should be a string'})
    @IsEmail({}, {message: "Is not mail"})
    readonly email: string;
    @ApiProperty({example: '12345', description: 'password'})
    @IsString({message: 'Should be a string'})
    @Length(4, 16, {message: 'The length of password should be between 4 and 16'})
    readonly password: string;
}
``` 
Here we check user login input data. We make sure, that mail string is actually an email and limit the length of the password string.

---

### Conclusion

---
**It is neccessary to validate any user's input data.**

---

