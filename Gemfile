source "https://rubygems.org"

# GitHub Pages-supported Jekyll. Pinned to the GitHub Pages gem so the
# locally-built site matches what GitHub Pages produces in production.
gem "github-pages", group: :jekyll_plugins

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
end

# Windows / JRuby tzinfo workaround (harmless on macOS)
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end
