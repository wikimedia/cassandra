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
    
    commit c4dda2525fbe3c1f6f29fea8afa5bb6249d24070
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 13:17:47 2018 -0500
    
        prompt compiler to use utf-8 source encoding
    
    commit feb033b34195ad993b57ad5192dec4471fb58aa4
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 11:07:21 2018 -0500
    
        Update for 2.2.6-wmf3 Debian package release
    
    commit 3a5687f3d67240e0f6f260d9802b53ee52632e79
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:57:37 2018 -0500
    
        comment out startup test
        
        https://issues.apache.org/jira/browse/CASSANDRA-7254 added a pre-start
        invocation of the JVM that blocks when using the Prometheus JMX exporter.  This
        patch comments out this invocation, since the condition the test checks for
        should not be a problem in our environment.
        
        Bug: T186567
    
    commit 9e94b97694c36d85ffc86e6ef00043758252df0f
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:49:04 2018 -0500
    
        import WMF build (2.2.6-wmf2)
    
    commit e892e3e3ba1b687222915f1c4f523bb7d212d63f
    Author: Eric Evans <eevans@wikimedia.org>
    Date:   Mon Mar 12 10:51:54 2018 -0500
    
        README.wmf.md
    
