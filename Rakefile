# This file is part of the jump project
#
# Copyright (C) 2010 Flavio Castelli <flavio@castelli.name>
# Copyright (C) 2010 Giuseppe Capizzi <gcapizzi@gmail.com>
#
# jump is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# jump is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with Keep; if not, write to the
# Free Software Foundation, Inc.,
# 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301, USA.

require 'rake'
require 'rdoc/task'
require 'rake/testtask'

task :default => "test"

namespace :test do
  desc "Test all classes"
  Rake::TestTask.new(:all) do |t|
    t.libs << "test"
    t.pattern = 'test/*_test.rb'
    t.verbose = true
  end 
end

desc "Run all the unit tests"
task :test do
  Rake::Task["test:all"].invoke
end

desc 'Generate documentation.'
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = 'rdoc'
  rdoc.title    = 'jump'
  rdoc.options << '--line-numbers' << "--main" << "README.rdoc"
  rdoc.rdoc_files.include('README.rdoc')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name        = %q{jump}
    gem.summary     = %q{A bookmarking system for bash and zsh shells}
    gem.description = %q{Jump is a tool that allows you to quickly change
                       directories in the bash and zsh shells using bookmarks.
                       Thanks to Jump, you won't have to type those long paths anymore.

                       Jump was inspired by go-tool by ActiveState
                       (http://code.google.com/p/go-tool/).}

    gem.files        = FileList[ '[A-Z]*', 'lib/**/*.rb', 'test/**/*.rb',
                                 'bash_integration/**/*',
                                 'zsh_integration/**/*']
    gem.license      = ["MIT"]
    gem.require_path = 'lib'
    gem.bindir = 'bin'
    gem.executables = ['jump-bin']
    gem.test_files   = Dir[*['test/**/*_test.rb']]

    gem.extra_rdoc_files = ["README.rdoc"]
    gem.rdoc_options = ['--line-numbers', "--main", "README.rdoc"]

    gem.authors = ["Flavio Castelli", "Giuseppe Capizzi"]
    gem.email   = %w(flavio@castelli.name gcapizzi@gmail.com)
    gem.homepage = "http://github.com/flavio/jump"

    gem.add_dependency "terminal-table", '>= 1.4.4'
    gem.add_development_dependency "fakefs"

    gem.platform = Gem::Platform::RUBY
    gem.post_install_message = File.read('POST_INSTALL.txt')
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler not available. Install it with: gem install jeweler"
end

desc "Clean files generated by rake tasks"
task :clobber => [:clobber_rdoc]
