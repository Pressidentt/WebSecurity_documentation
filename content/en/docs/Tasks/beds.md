---
title: "Data encryption"
date: 2017-01-05
weight: 2
description: >
 In that section we will talk about data privacy.
 It is very important to secure of both web-service itself and users' private data.
 For that, we will show encryption of users passwords.

---
 In that section we will talk about data privacy.
 It is very important to secure of both web-service itself and users' private data.
 For that, we will show encryption of users passwords.


### Encryption
In the given demo, go to auth service, here you can find *async registration()*

---

```js

        const candidate = await this.userService.getUserByEmail(userDto.email);
        if (candidate) {
            throw new HttpException('User with email already exists', HttpStatus.BAD_REQUEST);
        }
        const hashPassword = await bcrypt.hash(userDto.password, 5);

        const user = await this.userService.createUser({...userDto, password: hashPassword})
        if (user) {
            return user
        }
        return 'Registration was done successfully'
    
```

---
Here we use bcrypt library, which helps us to encrypt data. Bcrypt.hash function takes 2 arguments, the variable to encrypt: in our case password, and the number of rounds to secure the hash. The number commonly ranges from 5 to 15.


### Decryption

Encryption is done in registration part, now we will need to decrypt that data for logging part.
In the given demo, we stay at the same file, go to *async validateUser()*

---

```js

       const user = await this.userService.getUserByEmail(userDto.email);
        const passwordEquals = await bcrypt.compare(userDto.password, user.password);
        if (user && passwordEquals) {
            return user;
        }
        throw new UnauthorizedException({message: 'Wrong email or password'})
    }
    
```

---

Here we use bcrypt.compare function which compares given password input from user and saved hashed password in database.

