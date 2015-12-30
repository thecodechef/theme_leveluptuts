require 'yaml'
require 'json'

@config = YAML.load_file(File.join(File.dirname(__FILE__), 'config.yml'))
@pkg = JSON.load(File.join(File.dirname(__FILE__), 'package.json')) if File.exists?(File.join(File.dirname(__FILE__), 'package.json'))

if File.exists?(File.join(File.dirname(__FILE__), 'config.yml'))
  @version = @config[:version]
  @repo = @config[:repo]
else
  @version = @pkg[:version]
  @repo = @pkg[:repository]
end

namespace :git do

  desc "Initiates a Empty Git Repository in Current Directory"
  task :init do
    system "git init"
    system "touch README.md"
    system "touch LICENSE.md"
    system "touch CHANGLOG.md"
    system "touch CONTRIBUTING.md"
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

  desc "Creates a .git* Files"
  task :files do
    puts "Created ./.gitignore"
    sleep 1.2
    puts "Created ./.gitconfig"
    sleep 1.2
    puts "Created ./.gitaliases"
    sleep 0.2
    system "touch .gitignore"
    system "touch .gitconfig"
    system "touch .gitaliases"
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
    system "git push -u origin master"
  end

  namespace :tag do
    desc "Pushs Repository to GitHub with Tags"
    task :push do
      system "git tag -a v#{@version.to_s}"
      system "git push -u origin master --tags"
    end
  end

  namespace :remote do
    desc "Add a Remote Repository from GitHub"
    task :add do
      system "git remote add origin #{@repo}"
    end

    desc "Removes Remote from Repository"
    task :remove do
      system "git remote remove origin"
    end
  end

end