require 'rbconfig'
c = Config::CONFIG

def system!(cmd)
	puts cmd
	system(cmd) or raise
end

ver = '1.2.3'
core = "xapian-core-#{ver}"
bindings = "xapian-bindings-#{ver}"
xapian_config = "#{Dir.pwd}/#{core}/xapian-config"

task :default do
	[core,bindings].each do |x|
		system! "tar -xzvf #{x}.tar.gz"
	end

	prefix = Dir.pwd
  if c['target_os'] =~ /darwin/i
	  ENV['LDFLAGS'] = "-R#{prefix}/lib"
  end

	system! "mkdir -p lib"

	Dir.chdir core do
		system! "./configure --prefix=#{prefix} --exec-prefix=#{prefix}"
		system! "make clean all"
		system! "cp -r .libs/* ../lib/"
	end

	Dir.chdir bindings do
		ENV['RUBY'] ||= "#{c['bindir']}/#{c['RUBY_INSTALL_NAME']}"
		ENV['XAPIAN_CONFIG'] = xapian_config
		system! "./configure --prefix=#{prefix} --exec-prefix=#{prefix} --with-ruby"
		system! "make clean all"
	end

	system! "cp -r #{bindings}/ruby/.libs/_xapian.* lib"
	system! "cp #{bindings}/ruby/xapian.rb lib"
end
