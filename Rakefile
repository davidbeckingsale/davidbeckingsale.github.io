desc "Copy the argument to a new file in the _posts director, and add the necessary preamble"
task :new,[:name] do |t, args|
    filename = "#{Time.now.strftime('%Y-%m-%d')}-#{args.name.gsub(/BLOG/,'').gsub(/\\/,'').gsub(/\s/,'-').downcase}.md"
    path = File.join('_posts', filename)

    if File.exist? path; raise RuntimeError.new("Won't clobber #{path}");end

    File.open(path, 'w') do |file|
        file.write <<-EOS
---
layout: post
title: #{args.name.gsub(/BLOG/,'')} 
status: publish
type: post
excerpt: 
---
EOS
    end

    system("mvim #{path}")
end
