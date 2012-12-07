$:.unshift 'lib'
require 'rubygems'
require 'rake'
require 'rake/testtask'
require 'rdoc/task'
require 'rspec/core/rake_task'

task :default => "spec:suite"

begin
  require "jeweler"
  Jeweler::Tasks.new do |gemspec|
    gemspec.name        = "#{ENV["GEM_PREFIX"]}redis-store"
    gemspec.summary     = "Namespaced Rack::Session, Rack::Cache, I18n and cache Redis stores for Ruby web frameworks."
    gemspec.description = "Namespaced Rack::Session, Rack::Cache, I18n and cache Redis stores for Ruby web frameworks."
    gemspec.email       = "guidi.luca@gmail.com"
    gemspec.homepage    = "http://github.com/jodosha/redis-store"
    gemspec.authors     = [ "Luca Guidi" ]
    gemspec.executables = [ ]
    gemspec.add_dependency "redis", "~> 3.0.2"
    # BE: Depend on Rails 3.0
    gemspec.add_dependency "activesupport", "~> 3.0.5"
  end

  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler not available. Install it with: sudo gem install jeweler"
end

namespace :spec do
  desc "Run all the examples by starting a detached Redis instance"
  task :suite => :prepare do
    invoke_with_redis_replication "spec:run"
  end

  RSpec::Core::RakeTask.new(:run) do |t|
    t.pattern = 'spec/**/*_spec.rb'
    t.rspec_opts = %w(-fs --color)
  end
end

desc "Run all examples with RCov"
task :rcov => :prepare do
  invoke_with_redis_replication "rcov_run"
end

RSpec::Core::RakeTask.new(:rcov_run) do |t|
  t.pattern = 'spec/**/*_spec.rb'
  t.rcov = true
end

task :prepare do
  `mkdir -p tmp && rm tmp/*.rdb`
end

namespace :bundle do
  task :clean do
    system "rm -rf ~/.bundle/ ~/.gem/ .bundle/ Gemfile.lock"
  end
end

load "tasks/redis.tasks.rb"
