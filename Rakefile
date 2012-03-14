require 'rbconfig'
c = Config::CONFIG

def system!(cmd)
	puts cmd
	system(cmd) or raise
end

ver = '1.2.9'
core = "xapian-core-#{ver}"
bindings = "xapian-bindings-#{ver}"
xapian_config = "#{Dir.pwd}/#{core}/xapian-config"

task :default do
	[core,bindings].each do |x|
		system! "tar -xzvf #{x}.tar.gz"
	end

	prefix = Dir.pwd

	system! "mkdir -p lib"

	Dir.chdir core do
		system! "./configure --prefix=#{prefix} --exec-prefix=#{prefix}"
		ENV['LDFLAGS'] = "-R#{prefix}/lib"
		system! "make clean all"
		ENV['LDFLAGS'] = ""
		system! "cp -rL .libs/* ../lib/"
	end

	Dir.chdir bindings do
		ENV['RUBY'] ||= "#{c['bindir']}/#{c['RUBY_INSTALL_NAME']}"
		ENV['XAPIAN_CONFIG'] = xapian_config
		system! "./configure --prefix=#{prefix} --exec-prefix=#{prefix} --with-ruby"
		ENV['LDFLAGS'] = "-R#{prefix}/lib"
		system! "make clean all"
		ENV['LDFLAGS'] = ""
	end

	system! "cp -r #{bindings}/ruby/.libs/_xapian.* lib"
	system! "cp #{bindings}/ruby/xapian.rb lib"
end
