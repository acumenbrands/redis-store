source :gemcutter
gem "redis", "~> 3.0.2"
# BE: depend on AS at runtime so that we get a conflict if we try to upgrade to
# 3.1+
gem "activesupport", "~> 3.0.5"

group :development do
  gem "jeweler"
  gem "git"
end

group :development, :test, :rails3 do
  gem "rack-cache"
  gem "merb", "1.1.0"
  gem "rspec"
  gem "i18n"

  if RUBY_VERSION > '1.9'
    gem "methopara" # required by merb.
  else
    gem "ruby-debug" # linecache isn't compatible with 1.9.2 yet.
  end
end

group :rails3 do
  gem "rack", "~> 1.2.1"
  gem "actionpack", "~> 3.0.5"
end
