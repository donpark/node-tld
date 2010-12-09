# node-tld #

## Usage ##

### Get registered domain name ###

    var tld = require('tld');
    console.log(tld.registered('www.google.com')); // google.com
    console.log(tld.registered('www.anything.goes.fj')); // anything.goes.fj
    console.log(tld.registered('a.b.c.hyogo.jp')); // b.c.hyogo.jp
    console.log(tld.registered('api.metro.tokyo.jp')); // metro.tokyo.jp
    console.log(TLD.registered('www.foo.bar.sch.uk')); // foo.bar.sch.uk
    console.log(TLD.registered('www.british-library.uk')); // british-library.uk
  
### Hot update TLD data ###

Recent copy of TLD data is bundled within `node-tld` and loaded automatically on first call to `registered`. But if you want to hot update from an URL, following code will download TLD data from `node-tld`'s defaut TLD data source and, if parsed successfully, update in-memory TLD data cache. If `path` is provided, raw TLD data will also be saved to the location.

    var tld = require('tld');
    tld.download(
      'http://mxr.mozilla.org/mozilla-central/source/netwerk/dns/effective_tld_names.dat?raw=1',
      __dirname + '/effective_tld_names.dat');

### Load TLD data file from non-default path ###

If you downloaded more recent copy of TLD data to another path (perhaps using `download` method), you can either change `defaultFile` before first call to `registered` like this:

    var tld = require('tld');
    tld.defaultFile = '.../some/other/path/...';
    // first call triggers loads from above path
    tld.registered('foo.bar.com');

or load explicitly at anytime to switch/update TLD data:

    var tld = require('tld');
    tld.load('.../some/other/path/...');
    // first call triggers loads from above path
    tld.registered('foo.bar.com');
