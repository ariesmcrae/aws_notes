# IAM

* not region specific.

* Consists of users, groups, roles:
    1. User - person
    2. Group - collection of users with 1 set of permissions
    3. Role - can be applied to both users and AWS services (e.g EC2, Lambda)

* user access key id / secret access key is used for cli/api.

* MFA - Multi Factor Authentication

* newly created user by default has no permissions to do anything.
 
* permission is created by creating a policy or by using pre-built policies.

* a policy can be assigned to a :
    1. user
    2. group

* policy document language is **JSON**

* centralized conntrol of your AWS account

* Fin grained access control to AWS resources.



## Federated Active directory (SSO)
* Integrates with Active Directory, allowing SSO using **SAML** (Secure Assertive Markup Language).
    1. User navigates to ADFS webserver.
    2. User enters SSO creds
    3. User's browser receives SAML from ADFS.
    4. The user's browser posts the SAML AWS SAML endpoint signin.aws.amazon.com/saml. This is done by calling the **AssumeRoleWithSAML** API to request temporary security credentials.
    5. User is now able to access AWS console.


## Web Identity Federation
* Allows your (mobile) app to authenticate against AMZ, Google, Facebook.
1. Log in to Facebook first.
2. You are given ID token by FB.
3. Make API call **AssumeRoleWithWebIdentiy**, passing to it the FB ID token.
4. You are now granted temporary security to access AWS resource.

# Role and EC2 instances
* When you create an EC2 instance, you can optionally assign a role.
* You cannot change the IAM role on a running EC2 instance.
* You can change the permissions on the IAM role associated with a running EC2 instance, and the updated permissions will take affect almost immediately.
