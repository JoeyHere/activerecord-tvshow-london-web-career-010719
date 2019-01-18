# require_relative 'config/environment.rb'
#
# namespace :db do
#
#   # desc "Migrate the db"
#   # task :migrate do
#   #   connection_details = YAML::load(File.open('config/database.yml'))
#   #   ActiveRecord::Base.establish_connection(connection_details)
#   #   ActiveRecord::Migrator.migrate("db/migrate/")
#   # end
#
#   desc "drop and recreate the db"
#   task :reset => [:drop, :migrate]
#
#   desc "drop the db"
#   task :drop do
#     connection_details = YAML::load(File.open('config/database.yml'))
#     File.delete(connection_details.fetch('database')) if File.exist?(connection_details.fetch('database'))
#   end
#end

require 'active_record'
include ActiveRecord::Tasks

DatabaseTasks.db_dir = 'db'
DatabaseTasks.migrations_paths = ['db/migrate']

load 'active_record/railties/databases.rake'

task :console => :environment do
  Pry.start
end

task :environment do
  require_relative 'config/environment'
end

Rake::Task["db:drop"].clear

namespace :db do
  task :drop => :environment do
    puts "Dropping tables"
    File.delete('db/schema.rb')
    drop_db
  end
end
