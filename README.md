### webassets
---
https://github.com/miracle2k/webassets

```py
env = Environment(...)
env.version = 'hash'
env.versions = 'hash:32'
env.versions = 'timestamp'

env = Environment(...)
env.url_expire = True

bundle = Bundle(..., output='screen.%(version)s.css')

env = Environnment(...)
env.manifest = 'cache'

env = Environment(...)
env.manifest = 'file'
env.manifest = 'file://tmp/manifest.to-be-deployed'

child_bundle = Bundle('file.css', filters='yui_css')
Bundle(child_bundle, fileters='cssrewrite')

yui_css(cssrewrite(file.css))

cssrewrite.output(yui_css.output((cssrewrite.input((yui_css.input(file.css))))))

def noop(_in, out, **kw):
  out.write(_in.read())
  
bundle = Bundle('input.js', filters=(noop,))

{% assets filters=(noop, 'jsmin') ... %}

{% assets filters=my_filters ... %}

from webassets.filter import Filter

class NoopFilter(Filter):
  name = 'noop'
  
  def output(self, _in, out, **kwargs):
    out.write(_in.read())
  
  def input(self, _in, out, **kwargs):
    out.write(_in.read())

from webassets.filter import register_filter
register_filter(NoopFilter)

{% assets filters='jsmin,noop' ... %}

class FooFilter(Filter):
  def __init__(self, *args, **kwargs):
    self.args, self.kwargs = args, kwargs
  def unique(self):
    return self.args, self.kwargs

def unique(self):
  return id(self)

class FooFilter(Filter):
  def setup(self):
    import foolib
    self.foolib = foolib
    
  def apply(self, _in, out):
    self.foolib.convert(...)

class FooFilter(Filter):
  options = {
    'binary': 'FOO_BIN'
  }

class FooFilter(Filter):
  def setup(self):
    self.bin = self.get_config('BINARY_PATH')

self.get_config(setting='ASSETS_BINARY_PATH', env='BINARY_PATH')

self.get_config(setting='ASSETS_BINARY_PATH', env=False)

self.java = self.get_config('JAVA_BIN', require=False) or 'java'

less = Bundle('css/base.less', 'css/forms.less',
  filters='less,cssmin', output='screen.css')

sass = Bundle('*.sass', filters='sass', output='gen/sass.css')
all_css = Bundle('css/jquery.calendar.css', sass,
  filters='cssmin', output='gen/all.css')

from webassets.loaders import YAMLLoader
loader = YAMLLoader('asset.yml')
env = loader.load_environment()

env['some-bundle'].urls()
```

```
pip install -r requirements-dev.pip
pip install -r requirements-dev-2.pip
./requirements-dev.sh
./run_tests.sh
```

```
```


