Building Cassandra for Wikimedia
================================
   
### Cleanup any locally generated cruft

    $ rm -rf logs/ data/

### Create a release artifact in the expected format

    $ VERSION=2.2.6
    $ git archive --format=tar --prefix=cassandra-$VERSION/ \
            <treeish> | gzip > ../cassandra_$VERSION.orig.tar.gz

### Build a Debian package

    $ dpkg-buildpackage -rfakeroot -us -uc -i'\.git.*'

Delta to 2.2.6 (release)
-------------------------
    
    commit a9c95128eed6e1a60de891e6ddc7af47f6423fcf
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Thu May 31 16:55:45 2018 +0000
    
        Disable use of embedded Python driver
        
        See: https://issues.apache.org/jira/browse/CASSANDRA-11850
        
        Bug: T196044
    
    commit fc2b0a53e22bb4c9846b3193cd6475377fe3ee74
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Wed May 30 07:24:55 2018 -0500
    
        Update dependencies for Debian Stretch build
    
    commit a8bc50889890124f5fcbebfe4674c23f8c962e40
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Wed Mar 21 21:59:24 2018 +0000
    
        actually apply start-script patch in package build
        
        Bug: T186567
    
    commit e5407b29d9ffe4a67f98c8e913155785ba03aeed
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 13:17:47 2018 -0500
    
        prompt compiler to use utf-8 source encoding
    
    commit a4f5a092c8eb4a99cc9ec05bbaa839295fa6745f
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 11:07:21 2018 -0500
    
        Update for 2.2.6-wmf3 Debian package release
    
    commit f71bd6549fd85848c77f785eedca13c472f187d3
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:57:37 2018 -0500
    
        comment out startup test
        
        https://issues.apache.org/jira/browse/CASSANDRA-7254 added a pre-start
        invocation of the JVM that blocks when using the Prometheus JMX exporter.  This
        patch comments out this invocation, since the condition the test checks for
        should not be a problem in our environment.
        
        Bug: T186567
    
    commit 5d1d4a1d2911e46046ad18f2b832f8ebb6b508e6
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:49:04 2018 -0500
    
        import WMF build (2.2.6-wmf2)
    
    commit 225ee52cd53813bef1347e9a081c9b5c8cdbe74d
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:51:54 2018 -0500
    
        README.wmf.md
    