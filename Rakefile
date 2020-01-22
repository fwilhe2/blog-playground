autoload :FileUtils, 'fileutils'

desc 'Execute the middleman build command'
task :build do
  run 'middleman build --no-clean -e production'
end

namespace :deploy do
  desc 'Deploy to GitLab Pages from a GitLab CI build'
  task :gitlab do
    Rake::Task['build'].invoke
    FileUtils.cp_r 'config/meta/.', 'public'
  end
end

def run command, opts = {}
  system command
  unless $?.exitstatus.zero? || opts[:ignore_failure]
    raise %(Previous command exited with unexpected status code #{$?.exitstatus})
  end
end
