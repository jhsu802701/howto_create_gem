# Chapter 2: Git Repository

## credentials.sh

* Add the file credentials.sh to the root directory of your gem:
```
#!/bin/bash

# Output:
# First argument if it is not blank
# Second argument if first argument is blank
anti_blank () {
  if [ -z "$1" ]; then
    echo "$2"
  else
    echo "$1"
  fi
}

# Setting Git email if necessary
GIT_EMAIL="$(git config user.email)"
if [ -z "$GIT_EMAIL" ]; then
  EMAIL_DEF='you@example.com'
  echo
  echo "Default email address: ${EMAIL_DEF}"
  echo
  echo 'Enter your Git email address:'
  read EMAIL_SEL
  EMAIL=$(anti_blank $EMAIL_SEL $EMAIL_DEF)
  echo

  echo
  echo '------------------------------'
  echo "git config --global user.email"
  echo "$EMAIL"
  git config --global user.email "$EMAIL"
fi

# Setting Git name if necessary
GIT_NAME="$(git config user.name)"
if [ -z "$GIT_NAME" ]; then
  NAME_DEF='Your Name'
  echo
  echo "Default name: ${NAME_DEF}"
  echo
  echo 'Enter your Git name:'
  read NAME_SEL

  # NOTE: The double quotes are needed to avoid truncating the string
  # at the space.
  NAME=$(anti_blank "$NAME_SEL" "$NAME_DEF")

  echo
  echo '-----------------------------'
  echo "git config --global user.name"
  echo "$NAME"
  git config --global user.name "$NAME"
  echo
fi
```
* If you haven't already done so, use the "cd" command in Docker to enter the root directory of your app.
* Enter the command "sh credentials.sh".  If you haven't already done so, you will be prompted to enter your Git credentials.

## .gitignore
Add the following lines to the end of the .gitignore file:
```
*.gem
tmp*
.DS_Store
/log/
```

## Starting the Git Repository
* Enter the following commands:
```
git add .
git commit -m "Initial commit"
```
* Create a [GitHub](https://github.com/) repository for your gem's source code.
* Enter the following command:
```
git push origin master
```