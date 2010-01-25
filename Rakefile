require 'rubygems'
require 'rake'
require 'rubygems/ext'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "xapian-full"
    gem.version = '1.1.3'
    gem.summary = %Q{xapian-core + Ruby xapian-bindings}
    gem.description = %Q{Xapian bindings for Ruby without dependency on system Xapian library}
    gem.email = "rlane@club.cc.cmu.edu"
    #gem.homepage = "http://gitorious.org/holizz-projects/xapian-ruby"
    gem.authors = ["Tom Adams", "Rich Lane"]

    gem.files += Dir.glob(%w[
			extconf.rb
			Rakefile
			xapian*.tar.gz
    ])

    gem.extensions << 'extconf.rb'
  end
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: sudo gem install jeweler"
end
