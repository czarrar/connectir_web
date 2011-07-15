# Adopted from Scott Kyle's Rakefile
# http://github.com/appden/appden.github.com/blob/master/Rakefile

task :default => :server
 
desc 'Build site with Jekyll'
task :build do
  jekyll
end
 
desc 'Build and start server with --auto'
task :server do
  jekyll '--server --auto'
end

desc 'Build and deploy'
task :deploy => :build do
  sh 'rsync -avz --delete _site/ czarrar@www.nitrc.org:/home/groups/connectir/htdocs'
end

desc 'Build, deploy, and commit/push'
task :commit, :message do |t, args|
  msg = args[:message]
#  Rake::Task['deploy'].invoke
  sh "git commit -m '#{msg}'"
  sh 'git push'
end

desc 'test'
task :test, :testme do |t, args|
  response = args[:testme]
  puts response
  puts "When I say Rake, you say '#{response}'!"
end

def jekyll(opts = '')
  sh 'rm -rf _site'
  sh 'jekyll ' + opts
end
