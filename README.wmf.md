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

    commit 118ae3b0b9f94b07b618a8ecf10bed9bbca45149
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Thu Aug 10 17:51:00 2017 -0400
    
        Update for 3.11.0-wmf5 Debian package release
    
    commit baa7c52679f7059d5945bfeca5a01c1dde3f628f
    Author: Jeff Jirsa <jjirsa@apple.com>
    Date:   Tue Aug 29 10:31:16 2017 -0700
    
        StreamingHistogram is not thread safe
        
        Patch by Jeff Jirsa; Reviewed by Jason Brown, Marcus Eriksson  for CASSANDRA-13756
    
    commit 7168f5b336ba07543de9bd734fa4920402c3adb1
    Author: Robert Stupp <snazy@snazy.de>
    Date:   Fri Sep 1 19:11:32 2017 +0200
    
        BTree.Builder memory leak
        
        patch by Robert Stupp; reviewed by Jeremiah Jordan for CASSANDRA-13754
    
    commit 37bde164d701b7270fcf8814d620c0df9895fd1f
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
    
    commit 7fe6c971c475c5058bc4a1294de44f8e488c7ced
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Thu Aug 10 17:33:22 2017 -0400
    
        README.wmf.md
    
