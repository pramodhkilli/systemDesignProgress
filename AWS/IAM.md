# IAM

IAM : Identity and Access Management

Identity X wants to perform action y on resource z, should we allow it or not, it is decided by IAM

I might get confused again if i am reading this again, but the user here is not the end user, it is a developer or devops or non tech person or even our springboot application, does these users have permission to view or perform certain operation on a certain resource is the question

![alt text](DB/IAM1.png)

By default in AWS, every API call is denied by default, if we want someone to access a resource, then we have to explicitly grant the permission, this is where IAM comes into picture

** root user has unlimited power, it has even the power to delete the account, that is why using the root user credentials across a team is extremely riskly because everyone gets unrestricted access with no proper isolation or accountability

IAM Entities :

1. USER :

    as mentioned earlier, user can be a application, long lived program, or even a human like developer, devops, each user has a unique identifier called the ARN(Amazon Resource Name), and we can have user name and password, or if you want to use this in an application, then we can get access key id and secret key as well and each user has certain permissions

2. Policy :

    a. Identity Based policies : Policy is attached with IAM entity(user/group/role)

    basically in a policy, we have the policy language version, and then array of rules, rules contain things like effect(allow/deny), action(s3:getObject-which api or function you want to access for), resource(in a particular service there can be multiple resources, s3 is a service, in s3 we might have different resouces like dev, prod)

    b. Resource Based policies : the policy is attached to the resource

    apart from the effect, action and resource, we have priciple in resource based policies which has information regarding who can access or what users are allowed to access this resource

    Generally the flow goes like this, if a request comes, it checks in the policies if explicit deny is there, if so, that flow will be denied, if there is no explicit deny, then it will check if explicit allow is there, if it is not there, then it will be dropped, if it is there only, then it is allowed

    imagine a situation where for a resource you have both allow and deny policies for a user, this is a conflict, but if we go through the flow, as there is a deny, the flow will be dropped

3. Group :

    group is basically a container for users, lets say you have a policy you want to assign it to a group of people, you can assign it to a group instead, and you can make that user a part of that group, this way you dont have to assign n times if n users are there, make the n users part of that group, and assin this to the group, like backend developers group, or a particular team like finance, devops something like that

4. Role :

    IAM Role provides temporary identity, Instead of storing long-lived AWS Access and Secret keys(which might cause security issues), Users/Services can ASSUME a Role and user its credentials

    eg : you have an intern which has only READ access on S3, and you have a SDE3 which has both read and write access on S3, lets say we need to provide Intern all permissions which SDE3 has for 1 hour, how can we achieve this??? yeah through role

    we create a role called SeniorSDERole, attach all the permission which SeniorSDE should have with this role, maintain the list of identities which can use this role, otherwise anyone can just use this role, 