ip_finder Cookbook
================

This library cookbook adds the class `Chef::IPFinder`. It allows you to find IP addresses in a specific node, given an IP scope or a network interface. It also has some utility methods to discover all the IP addresses in a node, or to guess the scope of a given ip address.


Usage
-----

You must include the recipe `ip_finder::default` in the node's run list before using `Chef::IPFinder`.


### Finding IP addresses by scope

`Chef::IPFinder` supports finding IP addresses by a list of properties called scope. Properties can be  IP protocol version (ie. ipv4, ipv6), network addressing private, global, multicast, unicast, etc.

For instance, you can build queries like these:

Find all IPv4 addresses belonging to a private network:

```ruby
IPFinder.find(node, :private_ipv4)
#=> ['10.2.123.14', '192.168.1.14']
```

Find a public IPv6 address:
```ruby
IPFinder.find_one(node, :public_ipv6)
#=> '2600:3c00::f03c:91ff:fedf:f63c'
```

Find a multicast IPv4 address:
```ruby
IPFinder.find_one(node, :multicast_ipv4)
#=> '239.12.11.123'
```

Find all IPv4 addresses in node separated by scope:
```ruby
IPFinder.find_all(node)
#=> { "node" => ["127.0.0.1"], "private" => ["10.20.112.32"], "public" => ["200.23.142.11"] }
```

Find all IPv6 addresses in node separated by scope:
```ruby
IPFinder.find_all(node, :ipv6)
#=> { "public" => "2600:3c00::f03c:91ff:fedf:f63c" }
```

### Finding IP addresses by network interface

You can find IP addresses attached to a certain network interface like so:

Find a private IPv4 address attached to `eth1`:
```ruby
IPFinder.find_by_interface(node, 'eth1', :private_ipv4)
#=> '192.168.1.14'
```

Find an IPv6 address attached to `eth0`:
```ruby
IPFinder.find_by_interface(node, 'eth0', :ipv6)
#=> '2600:3c00::f03c:91ff:fedf:f63c'
```

Find an IPv4 address attached to the loopback interface `lo`:

```ruby
IPFinder.find_by_interface(node, 'lo')
#=> '127.0.0.1'
```


License
-------

Copyright (c) 2013 Restorando

MIT License

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

