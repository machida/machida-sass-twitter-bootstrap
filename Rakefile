require 'rubygems'
require 'bundler'
begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  $stderr.puts e.message
  $stderr.puts "Run `bundle install` to install missing gems"
  exit e.status_code
end
require 'rake'

VERSION = "1.3.0"
BOOTSTRAP_CSS = "bootstrap-#{VERSION}.css" 
BOOTSTRAP_MIN_CSS = "bootstrap-#{VERSION}.min.css" 

SASS_COMMAND = "sass --load-path lib --style"

desc'aaa'
task BOOTSTRAP_CSS do |target|
  sh "#{SASS_COMMAND} expanded lib/bootstrap.scss:#{target}"
  css = IO.read(target.to_s)
  css.gsub!('@DATE', `date`.strip)
  File.open(target.to_s, 'w+') { |f| f.write(css) }
end

desc'bbb'
task BOOTSTRAP_MIN_CSS do |target|
  sh "#{SASS_COMMAND} compressed lib/bootstrap.scss:#{target}"
end

desc "build regular and compresed versions of bootstrap"
task :build => [BOOTSTRAP_CSS, BOOTSTRAP_MIN_CSS]

desc "rebuild regular version of bootstrap when modifications are made"
task :watch do
  sh "expanded --watch lib/bootstrap.scss:#{BOOTSTRAP_CSS}"
end

task :default => :build
