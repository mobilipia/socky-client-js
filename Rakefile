# -*- coding: utf-8 -*-
task :default => [:compile]

desc 'Merge all socky submodules into one file.'
task :compile do

  require 'fileutils'
  # $:.unshift File.join(File.dirname(__FILE__),'..')

  scripts = [
             "socky.core.js",
             "json2.js",
             "vendor/web-socket-js/swfobject.js",
             "vendor/web-socket-js/FABridge.js",
             "vendor/web-socket-js/web_socket.js"
            ]

  assets = [
            "vendor/web-socket-js/WebSocketMain.swf",
            "vendor/web-socket-js/WebSocketMainInsecure.zip"
           ]

  version = File.read('VERSION')

  content = <<EOF
/**
 * Socky push-server JavaScript client
 *
 * @version #{version}
 * @author  Bernard Potocki <bernard.potocki@imanel.org>
 * @license The MIT license.
 * @source  http://github.com/socky/socky-js
 *
 */

EOF

  puts 'Reading files…'

  scripts.each do |script|
    path = 'lib/' + script
    puts ' + ' + path
    content += File.read(path) + "\n"
  end

  puts 'Generating…'

  puts ' + socky.js'
  File.open('socky.js', 'w') { |f| f.write(content) }

  puts 'Moving other assets…'

  assets.each do |asset|
    path = 'lib/' + asset
    puts ' + ' + path
    FileUtils.copy path, '.'
  end

  puts 'All done!'
end