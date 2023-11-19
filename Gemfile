# frozen_string_literal: true

source "https://rubygems.org"
gemspec

if RUBY_VERSION < "3"
  gem "minitest", "5.20.0"
else
  gem "minitest", "5.20.0"
end

# We need a newish Rake since Active Job sets its test tasks' descriptions.
gem "rake", "13.0.6"

gem "sprockets-rails", "3.4.2"
gem "propshaft", "0.6.4"
gem "capybara", "3.39.2"
if RUBY_VERSION < "3"
  gem "selenium-webdriver", "4.11.0"
  gem "webdrivers"
else
  gem "selenium-webdriver", "4.11.0"
end

gem "rack-cache", "1.14.0"
gem "stimulus-rails"
gem "turbo-rails"
gem "jsbundling-rails"
gem "cssbundling-rails"
gem "importmap-rails", "1.2.3"
gem "tailwindcss-rails"
gem "dartsass-rails"
# require: false so bcrypt is loaded only when has_secure_password is used.
# This is to avoid Active Model (and by extension the entire framework)
# being dependent on a binary library.
gem "bcrypt", "3.1.18", require: false

# This needs to be with require false to avoid it being automatically loaded by
# sprockets.
gem "terser", "1.1.13", require: false

# Explicitly avoid 1.x that doesn't support Ruby 2.4+
gem "json", "2.6.3"

# Workaround until Ruby ships with cgi version 0.3.6 or higher.
gem "cgi", "0.3.6", require: false

group :lint do
  gem "syntax_tree", "6.1.1", require: false
end

group :rubocop do
  gem "rubocop", "1.57.0", require: false
  gem "rubocop-minitest", require: false
  gem "rubocop-packaging", require: false
  gem "rubocop-performance", require: false
  gem "rubocop-rails", require: false
  gem "rubocop-md", require: false
end

group :mdl do
  gem "mdl", require: false
end

group :doc do
  gem "sdoc", git: "https://github.com/rails/sdoc.git", branch: "main"
  gem "rdoc", "6.6.0"
  gem "redcarpet", "3.5.1", platforms: :ruby
  gem "w3c_validators", "1.3.7"
  gem "rouge"
  gem "rubyzip", "2.3.2"
end

# Active Support
gem "dalli", "3.2.3"
gem "listen", "3.8.0", require: false
gem "libxml-ruby", platforms: :ruby
gem "connection_pool", require: false
gem "rexml", require: false
gem "msgpack", "1.7.0", require: false

# for railties
gem "bootsnap", "1.15.0", require: false
gem "webrick", require: false
gem "jbuilder", require: false
gem "web-console", require: false

# Action Pack and railties
rack_version = ENV.fetch("RACK", "~> 3.0")
if rack_version != "head"
  gem "rack", rack_version
else
  gem "rack", git: "https://github.com/rack/rack.git", branch: "main"
end

# Active Job
group :job do
  gem "resque", require: false
  gem "resque-scheduler", require: false
  gem "sidekiq", require: false
  gem "sucker_punch", require: false
  gem "delayed_job", require: false
  gem "queue_classic", "4.0.0", require: false, platforms: :ruby
  gem "sneakers", require: false
  gem "backburner", require: false
  gem "delayed_job_active_record", require: false
end

# Action Cable
group :cable do
  gem "puma", "6.3.1", require: false

  gem "redis", "5.0.5", require: false

  gem "redis-namespace"

  gem "websocket-client-simple", github: "matthewd/websocket-client-simple", branch: "close-race", require: false
end

# Active Storage
group :storage do
  gem "aws-sdk-s3", require: false
  gem "google-cloud-storage", "1.44.0", require: false
  gem "azure-storage-blob", "2.0.3", require: false

  gem "image_processing", "1.12.2"
end

# Action Mailbox
gem "aws-sdk-sns", require: false
gem "webmock"

# Add your own local bundler stuff.
local_gemfile = File.expand_path(".Gemfile", __dir__)
instance_eval File.read local_gemfile if File.exist? local_gemfile

group :test do
  gem "minitest-bisect"
  gem "minitest-ci", require: false
  gem "minitest-retry"

  platforms :mri do
    gem "stackprof"
    gem "debug", "1.7.1", require: false
  end

  gem "benchmark-ips"
end

platforms :ruby, :windows do
  gem "nokogiri", "1.15.4"

  # Needed for compiling the ActionDispatch::Journey parser.
  gem "racc", "1.7.3", require: false

  # Active Record.
  gem "sqlite3", "1.6.6"

  group :db do
    gem "pg", "1.5.3"
    gem "mysql2", "0.5.5"
    gem "trilogy", "2.5.0"
  end
end

platforms :jruby do
  if ENV["AR_JDBC"]
    gem "activerecord-jdbcsqlite3-adapter", github: "jruby/activerecord-jdbc-adapter", branch: "master"
    group :db do
      gem "activerecord-jdbcmysql-adapter", github: "jruby/activerecord-jdbc-adapter", branch: "master"
      gem "activerecord-jdbcpostgresql-adapter", github: "jruby/activerecord-jdbc-adapter", branch: "master"
    end
  else
    gem "activerecord-jdbcsqlite3-adapter", "70.1-java"
    group :db do
      gem "activerecord-jdbcmysql-adapter", "70.1-java"
      gem "activerecord-jdbcpostgresql-adapter", "70.1-java"
    end
  end
end

# Gems that are necessary for Active Record tests with Oracle.
if ENV["ORACLE_ENHANCED"]
  platforms :ruby do
    gem "ruby-oci8", "2.2.12"
  end
  gem "activerecord-oracle_enhanced-adapter", github: "rsim/oracle-enhanced", branch: "master"
end

gem "tzinfo-data", platforms: [:windows, :jruby]
gem "wdm", "0.1.1", platforms: [:windows]

# The error_highlight gem only works on CRuby 3.1 or later.
# Also, Rails depends on a new API available since error_highlight 0.4.0.
# (Note that Ruby 3.1 bundles error_highlight 0.3.0.)
if RUBY_VERSION >= "3.1" && RUBY_VERSION < "3.2"
  gem "error_highlight", "0.5.1", platforms: [:ruby]
end
