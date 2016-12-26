# IAM

* Without IAM, orgs with many users will sign up to AWS individually, then manage their own billing.
* Alternatively, one root account is shared among many people, which is a bad practice.
* IAM enables orgs to create multiple users, so that the root account is never used for day-to-day use.

* IAM has no additional charge for use.

* IAM AWS Account is global (not region specific).

* IAM policies can be directly attached to roles, users and groups. 
  Policies can only be applied to other AWS services (indirectly) through roles. 
  e.g. If EC2 instance wants to access S3, you attach a role to EC2. The role can have AmazonS3FullAccess permission.


* Consists of users, groups, roles:
    1. User - person
    2. Group - collection of users with 1 set of permissions (e.g. DEV). You add permission to DEV. e.g. Add AmazonS3FullAccess permission to DEV so that users in DEV could access S3.
    3. Role - allows AWS services to access other AWS services.
       e.g. You want EC2 instance to access S3. You create a role named EC2Role. You add AmazonS3FullAccess permission to the EC2Role.
       When you launch your EC2 instance, you assign EC2Role to that instance.

* Principle of least privilage - by default, access is denied to a newly created user. Access is granted through 'explicit allow'. 
  Eg. If Bob user is newly created and wants to access an S3 bucket, he won't be able to, because he is blocked by default.
  However, if you attach an AmazonS3FullAccess policy to user Bob, he'd be able to access it.

* user access key id / secret access key is used for cli/api. 

* MFA - Multi Factor Authentication

* permission is created by creating a policy or by using pre-built policies (grouping of permissions).

* a policy can be assigned to a :
    1. user
    2. group

* policy document language is **JSON**

* centralized conntrol of your AWS account

* Fine grained access control to AWS resources.

* ARN format arn:aws:service:region:account:resource
* eg.        arn:aws:iam    ::      1234567:user/cloud

* Limits:
  1. One Account = max 20 EC2 instances. You can't associate >1 role to an instance.
  2. 250 roles
  3. total policies size <= 10KB
  4. 1 group can have max = 10 policies.

* For an IAM user to launch an EC2 instance, it must be given 2 permissions in a role:
    1. Permission to launch
    2. Permission to associate role with the EC2 instance.

## Federated Active directory (SSO)
* Federated = externally authenticated
* Integrates with Active Directory, allowing SSO using **SAML** (Secure Assertive Markup Language).
    1. User navigates to ADFS webserver.
    2. User enters SSO creds
    3. User's browser receives SAML from ADFS.
    4. The user's browser posts the SAML AWS SAML endpoint signin.aws.amazon.com/saml. This is done by calling the **AssumeRoleWithSAML** API to request temporary security credentials.
    5. User is now able to access AWS console.
* GetFederationToken - allows IAM users to create Temporary Security Credentials for federated users.

## Web Identity Federation
* Allows your (mobile) app to authenticate against AMZ, Google, Facebook.
1. Log in to Facebook first.
2. You are given ID token by FB.
3. Make API call **AssumeRoleWithWebIdentiy**, passing to it the FB ID token.
4. You are now granted temporary security to access AWS resource.

## Role and EC2 instances
* When you create an EC2 instance, you can optionally assign a role.
* You cannot change the IAM role on a running EC2 instance.
* You can change the permissions on the IAM role associated while the EC2 instance is running. The updated permissions will take affect almost immediately.

## Root AWS Account Holder.
* Initially, your company would sign up for AWS. Whoever who signed up on behalf of the company is the Root AWS Account Holder.
* Instead of the company sharing that root account to some of its employees, the root AWS Account holder should set up an IAM admin group, as well as several users.
* Admin group would then be assigned to several users, so that root account would no longer need to be used to interact with AWS resources.
* Note: Root AWS Account holder is not linked to IAM, but could still interact with AWS resources.

### Q. A webapp in VPC is connected to corp data center via IPSec VPN. How can the webapp user access her S3 bucket using her IAM Role?
* App user authenticates against LDAP.
* The app retrieves her IAM role.
* App uses the IAM Security Token Service to assume that role.
* App then uses the temporary credentials to access her S3 bucket.

### Q. A webapp in VPC is connected to corp data center via IPSec VPN. How can the webapp user access her S3 bucket using her IAM user?
* Identity broker authenticates against LDAP.
* Using the IAM Security Token Service, the broker retrieves her IAM user.
* App calls the user's S3 bucket.



