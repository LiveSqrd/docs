Create a new Project
===

1. Go to https://dev-admin.lsq.io
2. Have a github account
3. Click + on admin panel after logging 
2. Enter a project name will be the subdomain 
3. Put a password for databases
4. Make a new github repo
5. Keep the repo empty and not init, will be fulled when created
5. Add lsqio as a collaborator under settings
6. Add webhook 
  * payload url https://dev-admin.lsq.io/project/(:projectname)/dev/gitpull
  * select push events
7. enter the ssh git repo info in the create form
8. Hit Create
9. Visit dev-(:projectname).lsq.io
