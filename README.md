1º Clone this repository.

    git clone https://github.com/mantecajc/docker-ruby-on-rails.git PROJECT_NAME

2º Give a project name in `.env` file. Please avoid blanks !

<!-- 3º Select your Ruby version on Dockerfile & Gemfile. -->

<!-- 4º Select your Rails version on Gemfile. -->

3º Run **docker-compose** from the directory containing the `docker-compose.yml` file:

    docker-compose run --no-deps webserver rails new . --force --database=postgresql

You should now have a Rails project in the app directory.

> For a [quick Rails install](https://www.bigbinary.com/blog/rails-6-1-adds-minimal-option-support), use the `--minimal` flag.

    docker-compose run --no-deps webserver rails new . --minimal --force --database=postgresql

4º Copy & paste `example.database.yml` on `database.yml`.

5º Builds project images & boots up the app.

    docker-compose build
    docker-compose up

7º Create database & run migrations.

    docker-compose run webserver rake db:create
    docker-compose run webserver rake db:migrate

Your Rails app is available at <http://localhost:3000/>

8º Disconnect your local repo from the remote:
    
    git remote rm origin
