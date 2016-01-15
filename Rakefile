# -*- coding: utf-8 -*-
# -*- mode: ruby -*-
# vim: ts=2:sw=2:expandtab:ft=ruby

require 'rake'
require 'rake/clean'
require 'fileutils'

directory 'cookbooks'
directory 'pkg'

pkgname = File.basename(Dir.pwd)

desc "Artifact cleaner"
def artclean(cpath)
    # Clean git
    Dir.glob("#{cpath}/**/.git").each{|gd| FileUtils.rm_rf gd}
    # Clean Gemfile.lock
    Dir.glob("#{cpath}/**/Gemfile.lock").each{|gd| FileUtils.rm_rf gd}
    # Clean Mac OS X tar — PaxHeader folder
    Dir.glob("#{cpath}/**/PaxHeader").each{|gd| FileUtils.rm_rf gd}
end

desc "Populate cookbooks"
task :berkshelf  do
    sh "bundle check || bundle install"
    FileUtils.rm_rf "cookbooks"
    sh "bundle exec berks vendor cookbooks"
    artclean "cookbooks"
end

desc "Prepare and pack chef bundle"
task :pack => ["berkshelf", "pkg"] do
      sh "tar -czf pkg/#{pkgname}.tar.gz cookbooks conf roles data_bags nodes site-cookbooks Rakefile"
end

desc "Regenerate cookbooks"
task :regen  do
    sh "rm -f Berksfile.lock"
    Rake::Task["berkshelf"].execute
    Rake::Task["pack"].execute
end

desc "Prepare dev env"
task :default => ["berkshelf"]
#task :default => ["berkshelf", "pack"]
