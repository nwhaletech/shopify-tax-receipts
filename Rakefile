require 'sinatra/activerecord/rake'
require 'resque/tasks'
require 'rake/testtask'
require './lib/app'

task :server do
  #SinatraApp.run!
  pipe = IO.popen("bundle exec rackup config.ru -p 4567")
  while (line = pipe.gets)
    print line
  end
end

task :deploy do
  pipe = IO.popen("git push heroku master --force")
  while (line = pipe.gets)
    print line
  end
end

task :clear_shops do
  Shop.delete_all
end

task :creds2heroku do
  Bundler.with_clean_env {
    api_key = `sed -n '1p' .env`
    shared_secret = `sed -n '2p' .env`
    secret = `sed -n '3p' .env`

    `heroku config:set #{api_key}`
    `heroku config:set #{shared_secret}`
    `heroku config:set #{secret}`
  }
end