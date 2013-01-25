Hike
====

Hike is a Ruby library for finding files in a set of paths. Use it to
implement search paths, load paths, and the like.

# Examples

Find Ruby files in this project:

    trail = Hike::Trail.new "/Users/sam/Projects/hike"
    trail.append_extension ".rb"
    trail.append_paths "lib", "test"

    trail.find "hike/trail"
    # => "/Users/sam/Projects/hike/lib/hike/trail.rb"

    trail.find "test_trail"
    # => "/Users/sam/Projects/hike/test/test_trail.rb"

Explore your Ruby load path:

    trail = Hike::Trail.new "/"
    trail.append_extensions ".rb", ".bundle"
    trail.append_paths *$:

    trail.find "net/http"
    # => "/Users/sam/.rvm/rubies/ree-1.8.7-2010.02/lib/ruby/1.8/net/http.rb"

    trail.find "strscan"
    # => "/Users/sam/.rvm/rubies/ree-1.8.7-2010.02/lib/ruby/1.8/i686-darwin10.4.0/strscan.bundle"

Explore your shell path:

    trail = Hike::Trail.new "/"
    trail.append_paths *ENV["PATH"].split(":")

    trail.find "ls"
    # => "/bin/ls"

    trail.find "gem"
    # => "/Users/sam/.rvm/rubies/ree-1.8.7-2010.02/bin/gem"

## Must include parent option

If you want your logical paths to include the parent directory, you can use this option:

    trail = Hike::Trail.new ".", { :must_include_parent => true }
    trail.append_extension ".js"
    trail.append_paths "/opt/something/project1", "/tmp/foo/bar/project2"

    trail.find "project1/lib/bla.js"
    # => "/opt/something/project1/lib/bla.js"

    trail.find "project2/app.js"
    # => "/tmp/foo/bar/project2/app.js"
    

# Installation

    $ gem install hike

# License

Copyright (c) 2011 Sam Stephenson.

Released under the MIT license. See `LICENSE` for details.
