# Postgresql

## Install
$ brew install postgresql@17

Or whatever version number, for right now it is 17

To have it run and start at login
$ brew services start postgresql@17

To stop it
$ brew services stop postgresql@17

To add it to your PATH
$ echo 'export PATH="/opt/homebrew/opt/postgresql@17/bin:$PATH"' >> /Users/robertpatton/.bash_profile

## Create user
After installation and initial startup, there won't be any users.  With the PATH set as above, run
$ createuser -s postgres

which will create a user 'postgres'

## Install pgAdmin4
$ brew install --cask pgadmin4