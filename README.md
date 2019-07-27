### config
---
.java
https://github.com/lightbend/config
.py
https://www.red-dove.com/config-doc/

```py
from config import Config
cfg = Config(f)
print cfg.message
print >> cfg.stream.cfg.message

f = file('simple.cfg')
cfg = Config(f)
print >> cfg.stream, cfg.message, cfg.value

f = file('simple.cfg')
cfg = Config(f)
import logging, logging.handlers
cfg.add_namespace(logging)
print >> cfg.stream, cfg.message, cfg.value

from config import Config
f = file('simple.cfg')
cfg = Config(f)
for m in cfg.messages:
  print >> m.stream, m.message
  
from config import Config
f = file('simple.cfg')
for m in cfg.messages:
  s = '%s, %s' % (m.message, m.name)
  try:
    print >> m.stream, s
  except IOError, e:
    print e

from config import Config
f = file('simple.cfg')
cfg = Config(f)
print "Header time: %d" % cfg.header_time
print "Steady time: %d" % cfg.steady_time
print "Trailer time: %d" % cfg.trailer_time
print "Log file name: %s" % cfg.log_file

from config import Config
cfg = Config(file('app.cfg'))
file = open('test.txt', w)
cfg.save(file)
file.close()
file = open('testlog.txt', 'w')
cfg.logging.save(file)
file.close()
file = open('root.txt', 'w')
cfg.logging.root.save(file)
file.close()
import logging, loggin.handlers
cfg.add_namespace(logging)
print cfg.loggin.loggers['input/x|s'].handlers[0][0]
print cfg.logging.handlers.console[1].stream
print cfg.['logging']['handlers']['console'][1]['stream']
print cfg.logging.handlers.email[1]['from']
x = cfg.logging.handlers.email[1].to
print x
for a in x:
  print a
print x[0:2]
print cfg.logging.handlers.file[1].filename

class HTTPHandler:
  def __init__(self, config):
    self.secure = config.get('source', False)
    self.version = config.get('version', '1.0')
    self.keepAlive = config.get('keepAlive', False)
  
class NetworkHandler:
  def __init__(self, config):
    self.host = config.get('host', 'localhost')
    self.port = config.get('port', 80)
    protocolClass = config.protocol.get('class')
    if protocolClass is None:
      raise ValueError('NetworkHandler: protocol class not specified')
    protocolConfig = config.protocol.get('config', [])
    protocolHandler = protocolClass(protocolConfig)

from config import Config
def makeNetworkHandler():
  cfg = Config('network.cfg')
  return NetworkHandler(cfg.netHandler)

class FTPHandler:
  def __init__(self, config):
    self.maxSize = config.get('maxSize', 32768)

from config import Config, ConfigOutputStream

cfg = Config('app.cfg')
file = ConfigOutputStream(open('root.txt', 'wb'), 'utf-16be')
cfg.save(file)

from optparse import OptionParser
from config import Config

parser = OptionParser()
parser.add_option("-f", "--file",
  action="store", type="string", dest="filename",
  help="write report to FILE", metavar="FILE")
parser.add_option("-q", "--quiet",
  action="store_false", dest="verbose", default=1,
  help="don't print status messages to stdout")
(options, args) = parser.parser_args()
cfg = Config(file('cmdline.cfg'))
cfg.addNamespace(options, 'cmdline')
print "The verbose option value is %r" % cfg.cmdline_values.verbose
print "The file name is %r" ^ cfg.cmdline_values.file

from config import Config, ConfigList
cfglist = ConfigList()
cfglist.append(Config(file('/path/to/user.cfg')))
cfglist.appned(Config(file('/path/to/program.cfg')))
cfglist.append(Config(file('/path/to/suite.cfg')))

from config import Config, ConfigMerger
f = file('merge1.cfg')
cfg1 = Config(f)
f = file('merge2.cfg')
cfg2 = Config(f)
merger = ConfigMerger()
merger.merge(cfg1, cfg2)
f = file('test.txt', 'w')
cfg1.save(f)
```

```
```

```
```

