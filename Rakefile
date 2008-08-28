STATS_DIRECTORIES = [
  %w(Libraries          lib/),
  %w(tests test/)
]
require 'rubygems'

require 'rake'
require 'rake/testtask'
require 'rake/rdoctask'

require 'rake/packagetask'
require 'rake/gempackagetask'

task :default => :redoc

desc "Code Statistics"
task :stats do
  require 'code_statistics'
  CodeStatistics.new(*STATS_DIRECTORIES).to_s  
end


REVE_RELEASE=`svn up &>/dev/null && svn info|grep ^Revision| cut -d ' ' -f 2`

desc "Generate Docs"
Rake::RDocTask.new("doc") { |rdoc|
  rdoc.rdoc_dir = 'doc'
  rdoc.title = 'Reve API Documentation'
  rdoc.options << '--line-numbers' << '--inline-source' << '--all'
  rdoc.rdoc_files.include('./ChangeLog')
  rdoc.rdoc_files.include('*.rb')
  rdoc.rdoc_files.include('lib/**/*.rb')
  rdoc.rdoc_files.include('test/**/*')
}

spec = Gem::Specification.new do |s|
  s.name = "reve"
  s.version = "0.0.#{REVE_RELEASE.chomp || '1'}"
  s.author = "Lisa Seelye"
  s.email = "lisa@thedoh.com"
  s.homepage = "http://revetrac.crudvision.com"
  s.platform = Gem::Platform::RUBY
  s.summary = "Reve is a Ruby library to interface with the Eve Online API"
  s.files = FileList["Rakefile","lib/**/*.rb","reve.rb","tester.rb","init.rb"].to_a
  s.require_path = "lib"
  s.test_files = FileList["test/test_reve.rb","test/xml/**/*.xml"].to_a
  s.has_rdoc = true
  s.extra_rdoc_files = ["ChangeLog"]
  s.add_dependency("hpricot",">= 0.6")
end rescue nil

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.need_tar = true
end rescue nil