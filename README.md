## Introduction

This is a simple web application to support the admission process in the CS department at FSU. It is based on Rocket, the web framework for Rust. Rust is a (more) secure programming language.  

## Steps to deploy:
- Install the nightly rust and checkout the source code, build the release version of the server
- Create a directory for the server and copy the binary and related files to it
- Install `poppler-util`
- Allow the server to bind to privileged ports `setcap cap_net_bind_service=+ep server`
- Create a directory for the database and export it as `DATABASE_URL`
- Run the hash program compiled in the first step to create a new hash for your admin account
- Edit the `migration/init/up.sql` to included the hash and slat
- Run `diesel migration run` to create the database
- Generate a self-signed certificate `openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes`
- Start the server with `ROCKET_ENV=production ./server` under the Linux `screen` command. 

To use the site, you need to export the data from the Slate by creating a query that export the following fields: Ref
`Name, Birthdate, Academic Department, Plan, Admit Term, Application, External_Id, Age, Primary Citizenship, Sex, Email, School 1 Institution, School 1 Major, School 1 Degree, School 2 Institution, School 2 Major, School 2 Degree, TOEFL Total, TOEFL Listening (0-30), TOEFL Reading (0-30), TOEFL Structure/Written Expression, TOEFL Speaking (0-30), GRE Verbal (130-170), GRE Quantitative (130-170), 
GRE Analytical Writing (0-6)` for the complete applications to your department. Run the query and export the data as a csv. This list of applications can be imported to the internal admission web site. For each individual application, you then need to download the all-in-one PDF file that contains all the supporting materials and upload it. The server will automatically break the file into smaller files. 


