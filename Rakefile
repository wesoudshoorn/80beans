SSH_USER = 'matsimitsu'
SSH_HOST = 'blog.matsimitsu.com'
SSH_DIR  = '/home/matsimitsu/static'

desc "Build the website from source"
task :build do
  puts "## Building website"
  status = system("bundle exec middleman build --clean")
  puts status ? "OK" : "FAILED"
end

desc "Run the preview server at http://localhost:4567"
task :preview do
  system("bundle exec middleman server")
end

desc "Deploy website via rsync"
task :deploy do
  puts "## Deploying website via rsync to #{SSH_HOST}"
  status = system("rsync -avze 'ssh' --delete build/ #{SSH_USER}@#{SSH_HOST}:#{SSH_DIR}")
  puts status ? "OK" : "FAILED"
end

desc "Clean up the deploy"
task :cleanup do
  puts "## Cleaning build"
  status = system("rm -rf build")
  puts status ? "OK" : "FAILED"
end

desc "Build and deploy website"
task :build_deploy => [:build, :deploy, :cleanup] do
end
