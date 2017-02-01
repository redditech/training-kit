#!/usr/bin/env rake

desc "Clean up generated site"
task :clean do
  sh "rm -rf _site"
end

desc "Runs the tests!"
task :test do
  require "html-proofer"

  sh "bundle exec jekyll build"

  File.readlines("script/writewell-files.txt").each do |line|
    HTMLProofer.check_file(line.delete!("\n"), {
      :empty_alt_ignore => true,
      :external_only => true,
      :url_ignore  => [
        %r{https?://github.com/new},
        /\.github\.io/,
        /\.gitter\.im/,
        /atom\.io/,
        /git-scm\.com/,
        /github\.com/,
        /mademistakes\.com/,
        /nasa\.gov/,
        /travis-ci\.org/,
      ],
      :href_ignore => [],
      :href_swap => {},
      :connecttimeout => 600,
      :typhoeus => {
        :ssl_verifypeer => false,
        :ssl_verifyhost => 0,
        :followlocation => true
      }
    }).run
  end
end

task :default => [:test]
