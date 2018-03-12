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
        
    commit ab7621bfd8095c6035ad7065d2dc58cbc213dbf3
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Wed May 30 07:24:55 2018 -0500
    
        Update dependencies for Debian Stretch build
    
    commit 9b515b1c5e3641543744d9b7b6be3edf578419a1
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Wed Mar 21 21:59:24 2018 +0000
    
        actually apply start-script patch in package build
        
        Bug: T186567
    
    commit 40d107f4004041aa2cb5da22944334665dadc486
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 13:17:47 2018 -0500
    
        prompt compiler to use utf-8 source encoding
    
    commit 18fc804c1e588a5e0615d9aa217475810d54857f
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 11:07:21 2018 -0500
    
        Update for 2.2.6-wmf3 Debian package release
    
    commit b6556e5a1433629bd5325aa9e391e9efd2b78ff0
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:57:37 2018 -0500
    
        comment out startup test
        
        https://issues.apache.org/jira/browse/CASSANDRA-7254 added a pre-start
        invocation of the JVM that blocks when using the Prometheus JMX exporter.  This
        patch comments out this invocation, since the condition the test checks for
        should not be a problem in our environment.
        
        Bug: T186567
    
    commit cac4b417f390f04890959d1bd673da3c3be00a2c
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:49:04 2018 -0500
    
        import WMF build (2.2.6-wmf2)
    
    commit 5d84a0eaa66a7de0c59d4f57a2aa4b65d12b045c
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:51:54 2018 -0500
    
        README.wmf.md
    
