# Rakefile
desc 'deploy Jekyll site to Github Pages'
task :deploy do
  sh 'bundle exec jekyll clean'
  sh 'export JEKYLL_ENV=production; bundle exec jekyll build'
  sh 'echo simpleflatmapper.org > docs/CNAME'
  sh 'git add ./docs'
  sh 'git commit -m \'Update\''
  sh 'git push origin master'
end


