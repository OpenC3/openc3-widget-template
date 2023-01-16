# encoding: ascii-8bit

# Copyright 2023 OpenC3, Inc.
# All Rights Reserved.
#
# This file may also be used under the terms of a commercial license
# if purchased from OpenC3, Inc.

PLUGIN_NAME = Dir['*.gemspec'][0].split('.')[0..-2].join('.')

task :require_version do
  if ENV['VERSION']
    if ENV['VERSION'] =~ /-/
      # Add Timestamp to prerelease versions
      ENV['VERSION'] = ENV['VERSION'] + "." + Time.now.utc.strftime("%Y%m%d%H%M%S")
    end
  else
    puts "VERSION is required: rake <task> VERSION=X.X.X"
    exit 1
  end
end

task :build => [:require_version] do
  _, platform, *_ = RUBY_PLATFORM.split("-")
  if platform == 'mswin32' or platform == 'mingw32'
    puts "Warning: Building gem on Windows will lose file permissions"
  end
  success = system("yarn run build")
  raise "yarn run build failed" unless success
  system("gem build #{PLUGIN_NAME}")
end
