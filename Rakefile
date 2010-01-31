require 'rbconfig'
c = Config::CONFIG

def system!(cmd)
	puts cmd
	system(cmd) or raise
end

ver = '1.1.3'
core = "xapian-core-#{ver}"
bindings = "xapian-bindings-#{ver}"
xapian_config = "#{Dir.pwd}/#{core}/xapian-config"

task :default do
	[core,bindings].each do |x|
		system! "tar -xzvf #{x}.tar.gz"
	end

	Dir.chdir core do
		system! "./configure"
		system! "make clean all"
	end

	Dir.chdir bindings do
		ENV['RUBY'] ||= "#{c['bindir']}/#{c['RUBY_INSTALL_NAME']}"
		ENV['XAPIAN_CONFIG'] = xapian_config
		system! "./configure --with-ruby"
		system! "make clean all"
	end

	system! "mkdir -p lib"
	system! "cp #{bindings}/ruby/.libs/_xapian.* lib"
	system! "cp #{bindings}/ruby/xapian.rb lib"
end
