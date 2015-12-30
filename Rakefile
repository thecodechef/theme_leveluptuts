require 'yaml'
require 'json'

if File.exists?(File.join(File.dirname(__FILE__), 'config.yml'))
  @version = YAML.load_file(File.join(File.dirname(__FILE__), 'config.yml'))[:version]
  @repo = YAML.load_file(File.join(File.dirname(__FILE__), 'config.yml'))[:repo]
else
  @version = JSON.load_file(File.join(File.dirname(__FILE__), 'package.json'))[:version]
  @repo = JSON.load_file(File.join(File.dirname(__FILE__), 'package.json'))[:repository]
end

namespace :git do

  desc "Initiates a Empty Git Repository in Current Directory"
  task :init do
    system "git init"
  end

  desc "Gives current Status of Repository"
  task :status do
    system "git status"
  end

  desc "Add Files to Repository Stage"
  task :add do
    system "git add ."
    system "git status"
  end

  desc "Creates a .gitignore File"
  task :ignore do
    puts "Created .gitignore"
    sleep 1.2
    system "touch .gitignore"
  end

  desc "Commit Message for Repository"
  task :commit do
    puts "Commit Message: "
    system "git commit"
  end

  desc "Pulls Repository from Origin"
  task :pull do
    system "git pull"
  end

  desc "Pushs Repository to GitHub"
  task :push do
    system "git tag -a v#{@version.to_s}"
    system "git push -u origin master --tags"
  end

  namespace :remote do
    task :add do
      system "git remote add origin #{@repo}"
    end

    task :remove do
      system "git remote remove origin"
    end
  end

end