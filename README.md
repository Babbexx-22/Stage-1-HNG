## AUTOMATING USER AND GROUP MANAGEMENT WITH BASH SCRIPTING

## INTRODUCTION
In modern IT infrastructure management, automating routine tasks such as user and group management is essential for efficiency, consistency, and security. As a SysOps engineer, I developed a Bash script named create_users.sh to streamline the process of creating and managing user accounts on Linux systems.

## SCRIPT OVERVIEW
The create_users.sh script reads from an input file (name-of-inputfile) that contains usernames and associated groups in the specific format (user;groups). It performs several critical tasks:

1. Initial Setup
The script begins by checking if it is executed with root privileges, essential for performing administrative tasks. It also validates the presence of the input file and provides guidance if not provided.

2. File and Directory Management
To ensure operational integrity and security, the script ensures that necessary log and password files are in place with correct permissions:
/var/log/user_management.log for logging all script activities.
/var/secure/user_passwords.txt for securely storing generated passwords.

3. User and Group Creation
For each line in the input file:
- Primary Group Creation: Checks if a group with the same name as the username exists. If not, it creates a new group using groupadd. This serves as the personal group for each user
- User Creation: Adds users (useradd) with their primary groups, ensuring home directories are created for each users using the (-m flag).
- Additional Group Assignment: Adds users to supplementary groups specified in the input file using usermod -aG.

4. Password Management
Security is paramount in user account management:
- Password Generation: Generates random passwords using openssl rand -base64 12.
- Password Storage: Stores usernames and encrypted passwords in /var/secure/user_passwords.txt, maintaining confidentiality (chmod 600).

5. Logging and Error Handling
- Logging: Utilizes a custom function log_message() to record each action with timestamps in /var/log/user_management.log.
- Error Handling: Manages scenarios such as existing users or groups gracefully, ensuring robustness and reliability in operations.

## USAGE AND TESTING

- To execute the script, run the following command: `sudo bash create_users.sh name-of-text-file`
  Replace "name-of-text-file" with the path to the input file containing user and group data.


## TESTING

- Log Verification: Review /var/log/user_management.log to confirm all operations are logged correctly.
- Password File Inspection: Check /var/secure/user_passwords.txt to ensure passwords are securely stored.
- User Verification: Validate user and group creation as per specifications in the input file.

## CONCLUSION

By automating user and group management with create_users.sh, SysOps engineers can enhance operational efficiency, maintain consistent security practices, and reduce manual errors in system administration. This script serves as a robust tool for scaling user management tasks across Linux environments.
