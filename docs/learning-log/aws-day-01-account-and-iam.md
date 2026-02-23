# AWS Day 01 – Account and IAM Foundations  
**Date:** 21 February 2026

---

## Topics Covered
- AWS Account Model
- Root User & MFA
- IAM Fundamentals
- Access Keys
- AWS CLI Configuration

---

## Key Concepts
- The AWS account acts like a container for identities (users) and resources. A unique email add and a credit card are needed to create one. The ACCOUNT ROOT USER can be the only user to access this account and has unrestricted previledges by default. 
- It is essentially a pay-as-you consume cloud platform that facilitates the use of the Amazon Simple Storage Service (S3) and the Elastic Compute Cloud (EC2, i.e., the virtual server in the cloud which runs apps, APIs, databases, software, etc.).
- Security: Additional identities can be created that can be restricted via IAM
- IAM: Identity and Access Management -> allows the creation of other identity types i.e., Users, Roles and Groups where full or limited permissions can be allowed -> therefore enabling security.
- The AWS account acts like a container -> so that any security issues can be contained/ or isolated or restricted to the root user -> therefore limiting the blast radius.
- External identities in other AWS accounts or other networks are denied access to these identities by default except for the ACCOUNT ROOT USER.

- WE can apply Multi-Factor Authentication (MFA) to the Root User Account and to the identities. MFAs are pieces of evidence which prove identity, e.g.,
    1. Knowledge - something you know (username, password)
    2. Possession - something you have (bank card, MFA device /app)
    3. Inherent - something you are (finger print, face, voice, iris)
    4. Location - A physical location, eg, which network (corportate network or home WiFi)


- IAM has all the authorisations /permissions that the AWS Account and the account root user has. Identities start with No permissions (the architect should only allow permissions to the level of the job to be accomplished by the user - a concept knwon as LEAST PREVILEDGED ACCESS). Only the root user is fully trusted.
- * (AWS Account) -> Full trust -> (IAM, Identities)
      1. Uses (humans or applications)
      2. Groups (collections of related users)
      3. Roles (AWS services or external access) - uncertain external users, etc
      4. Policy document or object - IAM also allows the creation of policy documents to permit or deny access to AWS servcies when and only when they are attached to IAM users, groups and roles
   
  - Consequently, IAM fulfills the following three main roles
      1. MANAGE IDENTITIES: An ID provider (IDP) - lets you create, delete and modify identities such as users and roles
      2. AUTHENTICATE: prove you are who you claim to be
      3. AUTHORISE: permit or deny access to resources

  - BASICS of IAM
      * No cost
      * Enables global service and global resilience
      * Permits or denies its identities on its AWS account through policies
      * No direct control on external accounts or users
      * it lets you use IDENTITY FEDERATION and MFA [identity federation allows you to use identities you already have e.g., signin-in using facebook to access AWS resources.
   
  - IAM ACCESS KEYS
      * I have created an IAM user with Admin permissions and generated it's IAM access keys.
      * The AWS CLI can also be used to access IAM user identity
      * these are also referred to as "LONG-TERM CREDENTIAL2, i,e, they don't change regularly or rotate/ they dont change automaticall
   
        (User & password) -> USER <- (Command Line, Access keys)

      * IAM user has 1 username (public) and 1 password (private) but can have up to 2 access keys (none, 1, or 2), both can either be active or inactive
      * Access keys can be created, deleted, made inactive or active -> WHEN CREATED THEY DEFAULT TO BE IN AN ACTIVE STATE and they are formed from 2 parts - they have to be deactivated before deleting.
              1. Access key (NON sensitive)
              2. Secret Access Key (concealed for security reasons)
        * (both  parts of the credentials are provided when you create the Access Keys and they can only be downloaded once).
        * You alsos need to select what the intended use is (e.g., CLI, local code, 3rd party servoce, apps running on an AWS compute service or Apps running outside AWS?)
        * Set desciption tag - e.g. LOCAL CLI IAMADMIN-GENERAL
        * Can be regenerated -> creating a brand new set and update all applications and commandline utilities.
        * IAM users are the only identities that can use access keys (NOT roles or groups)
       
        * i HAVE created the ACCESS KEYS  for the IAM Admin User in the general AWS account.
       
    - INSTALLED THE CLI and configured the CLI with the access keys to interact the IA< user accounts throug the CLI
        * Download the AWS CLI https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
        * C:\Users\mrone>cd C:\

                    C:\>
                    C:\>aws
                    
                    aws: [ERROR]: the following arguments are required: command
                    
                    usage: aws [options] <command> <subcommand> [<subcommand> ...] [parameters]
                    To see help text, you can run:
                    
                      aws help
                      aws <command> help
                      aws <command> <subcommand> help
                    
                    
                    C:\>
                    C:\>

         * aws --version
         * Configure a named profile:
                 > aws configure --profile iamadmin-general
                 > AWS Access key ID [None]: <access key>
                 > AWS Secret Access Key [None]: <secret>
                 > Default region name [None]: us-east-1
                 > Default output format [None]:
                 >

        * TEST
                 > aws s3 ls
                    (unable to lacate credentials. You can configure credentials bu running "aws configure"
          . Because the credentials have been configures inside a named profile, we need to specify that named profile on the CLI -> the command should be as follows
                  > aws s3 ls --profile iamadmin-general
          ' No error, just an empty string because we haven't created any S3 buckets - it's still a new account.
        * DANGER
            - Anybody who has the secret access key and the access key can  utilise the      IAM idenity configured together with any permissions    that that idenity has over the AWS account - anyone with these crednetials can interract with the aws account because this had administraive permissions with disastroous resuts - storage and access need to be carefully guarded. delete them off the system since they are already configured with in the CLI app.
              - great day!!!
---

## Architectural Takeaways
  1. The AWS Account is not just a login container — it is the actual security boundary. Everything lives inside it (IAM, users, roles, services). Therefore, account design is the first architectural decision.
  2. The Root User feels powerful, but it is almost like an emergency identity. Architecturally, it should exist but never be part of day-to-day operations.
  3. IAM is not just about creating users. It is really about designing trust. Every permission granted is a deliberate decision that shapes the system’s security posture from the beginning.
  4. Least privilege is not just a best practice — it is structural discipline. If permissions are loose, the architecture inherits the weakness.
  5. Separation of identities (users, roles, groups) enables blast radius reduction. Security is structural, not optional.
  6. Long-term access keys feel convenient, but they create persistent risk. They should be minimised wherever possible or replaced with roles.
  7. Cloud architecture is not just about “clicking around in a console.” It is also programmable infrastructure.
  8. Identity clearly comes before networking, storage or compute. If identity is weak, nothing built on top of it is secure (permissions granted constitute design decisions with security and cost implications).

---

## Questions for Deeper Study
  1. Best practices for handling long-term credentials in production environments?
  2. When should you choose to use IAM users as opposed to using IAM roles
  3. How are the Access Control Lists (ACLs) I learned during my CCNA related to permission models within AWS IAM? Is there also an invisible implicit deny?
  4. What similarities exist between policy-based traffic control in QoS and identity-based access control in AWS IAM, and how do their enforcement layers differ?
  5. When is it valid to open multiple AWS accounts instead of one?
  6. How does identity federation look like in a production environment?
  
