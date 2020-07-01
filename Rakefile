require 'rake'
require 'rake/clean'
require 'rspec/core/rake_task'

CLEAN.include('**/*.tar', '**/*.zip', '**/*.gz', '**/*.bz2')
CLEAN.include('**/*.rbc', '**/*.gem', '**/*.tmp')

namespace 'gem' do
  desc 'Create the file-temp gem'
  task :create => [:clean] do
    require 'rubygems/package'
    spec = eval(IO.read('file-temp.gemspec'))
    spec.signing_key = File.join(Dir.home, '.ssh', 'gem-private_key.pem')
    Gem::Package.build(spec, true)
  end

  desc 'Install the file-temp gem'
  task :install => [:create] do
     file = Dir["*.gem"].first
     sh "gem install -l #{file}"
  end
end

desc 'Run the test suite for the file-temp library'
RSpec::Core::RakeTask.new(:spec)

task :default => :spec
