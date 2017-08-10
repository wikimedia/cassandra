Building Cassandra for Wikimedia
================================

Debian package
--------------

### Cleanup any locally generated cruft

    $ rm -rf logs/ data/

### Create a release artifact in the expected format

    $ VERSION=3.11.0
    $ git archive --format=tar --prefix=cassandra-$VERSION/ \
            <treeish> | gzip > ../cassandra_$VERSION.orig.tar.gz

### Build a Debian package

    $ dpkg-buildpackage -rfakeroot -us -uc -i'\.git\/.*'

Delta to 3.11.0 (release)
-------------------------

    commit 9751562de9bcad45a1d4357b414288af23b354f2
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Thu Aug 10 17:51:00 2017 -0400
    
        Update for 3.11.0-wmf4 Debian package release
    
    commit 893f498e49085513ab4c0193f964b7039db42e77
    Author: Robert Stupp <snazy@snazy.de>
    Date:   Fri Sep 1 19:11:32 2017 +0200
    
        BTree.Builder memory leak
        
        patch by Robert Stupp; reviewed by Jeremiah Jordan for CASSANDRA-13754
    
    commit 14b12fbae1aea9bf5a6fa309ccd57023e5e3f047
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Aug 7 16:05:50 2017 -0400
    
        Let the JVM dump heaps
        
        Cassandra examines trapped exceptions and attempts to generate it's
        own heap dump using `jmap` when encountering an
        `OutOfMemoryException`.  If `-XX:+HeapDumpOnOutOfMemoryError` is
        passed to the JVM (like we do in WMF production), it too will attempt
        to create a heapdump, race the invocation of `jvm`, and hilarity
        ensues.
        
        See: https://issues.apache.org/jira/browse/CASSANDRA-13006
        See: https://phabricator.wikimedia.org/T172384
    
    commit 3d48e0451fb36a6e9a35b15cb4a36f5b44399d52
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Thu Aug 10 17:33:22 2017 -0400
    
        README.wmf.md
    
