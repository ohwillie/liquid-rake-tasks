require 'fileutils'
require 'liquid'

TEMPLATES_DIR = 'templates'
SITE_DIR = 'site'

Liquid::Template.file_system =
  Liquid::LocalFileSystem.new(File.join(TEMPLATES_DIR, 'partials'))

task :build do
  FileUtils.mkdir_p(SITE_DIR)

  Dir[File.join(TEMPLATES_DIR, '*.liquid')].each do |file|
    content = File.read(file)
    result = Liquid::Template.parse(content).render
    basename = File.basename(file, '.liquid')
    out = File.join(SITE_DIR, "#{basename}.html")
    File.open(out, 'w') { |f| f.write(result) }
  end
end

task default: 'build'

task :clean do
  FileUtils.rm_rf(SITE_DIR)
end
