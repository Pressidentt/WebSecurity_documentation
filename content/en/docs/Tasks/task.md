---
title: "Access control"
date: 2017-01-05
weight: 5
description: >
  In this section, we will talk about access control.
---

## Role type access control
Often there is a need to limit access to some of Api's endpoints. For that, in our example, we will use Role type access control. Each user in database have role id. 

---

### Example 1
For example, we will need to get list of all users. We don't want to give that information to any user. It will be accessible only for our admins.

---
We go to users.controller
 ```js
    @ApiOperation({summary: 'Get all users, requires Admin token'})
    @ApiResponse({status: 200, type: [User]})
    @Roles("Admin")
    @UseGuards(RolesGuard)
    @Get()
    getAll() {
        return this.usersService.getAllUsers();
    }
``` 
As you can see above we use RolesGuard decorator, which will check the role of the user, and will give access only if role is Admin.

---

### Example 2
For example, we want to ban user for some reason. Obviously, we want to let only admin ban users.

---
In the same file:
 ```js
    @ApiOperation({summary: 'Ban user'})
    @ApiResponse({status: 200})
    @Roles("Admin")
    @UseGuards(RolesGuard)
    @Post('/ban')
    ban(@Body() dto: BanUserDto) {
        return this.usersService.ban(dto);
    }
``` 
---

### Conclusion
---
**In the similiar way we can make accessibe endpoints for specific range of users.**

---



