require 'rake'
require 'rubygems'
def rebar_verbose_flag
    ENV["VERBOSE"] && "-v"
end
task :default => :compile


desc "Run common tests"
task :test => :compile do
    ct_run("test")
end

desc "Compile"
task :compile  do
    rebar('compile')
end

def rebar(param_string)
  rebar = File.join(File.dirname(__FILE__), 'rebar')
  sh "\"#{rebar}\" #{param_string} #{rebar_verbose_flag}" do |ok, res|
      if ! ok
          message = "\e[0;31m \n\n************************************\n\t"
          message += "Something failed running: \e[m'rebar #{param_string}'"
          message += "\e[0;31m\n************************************\e[m"
          fail "#{message}"
      end
  end
end

def ct_run(param_string)
  rebar = File.join(File.dirname(__FILE__), 'rebar')
  sh "\"ct_run\" -noshell -pa ebin -ct_hooks cth_junit -logdir logs -dir #{param_string}" do |ok, res|
      if ! ok
          message = "\e[0;31m \n\n************************************\n\t"
          message += "Something failed running: \e[m'ct_unit #{param_string}'"
          message += "\e[0;31m\n************************************\e[m"
          fail "#{message}"
      end
  end
end
