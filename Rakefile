require 'yaml'
require 'json'

@config_file = File.join(File.dirname(__FILE__), 'config.yml')
@pkg_file = File.join(File.dirname(__FILE__), 'package.json')

@config = YAML.load_file(@config_file)
@pkg = JSON.load(@pkg_file) if File.exists?(@pkg_file)

if File.exists?(@config_file) && !File.exists?(@pkg_file)
  @version = @config[:version]
  @repo = @config[:repo][:url]
elsif File.exists?(@pkg_file) && !File.exists?(@config_file)
  @version = @pkg[:version]
  @repo = @pkg[:repository][:url]
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

  desc "Creates Standard GitHub Files"
  task :files do
    files = %w{ .gitignore README.md LICENSE.md CHANGELOG.md CONTRIBUTING.md TODO.md }
    files.each do |file|
      unless File.exists?(File.join(File.dirname(__FILE__),"#{file}"))
        system "touch #{file}"
      else
        puts "#{file} already exists."
      end
    end
  end

  desc "Commit Message for Repository"
  task :commit do
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