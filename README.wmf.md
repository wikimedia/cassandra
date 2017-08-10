Building Cassandra for Wikimedia
================================

Debian package
--------------

### Cleanup any locally generated cruft

    $ rm -rf logs/ data/

### Create a release artifact in the expected format

    $ VERSION=3.11.0
    $ git archive --format=tar --prefix=cassandra-$VERSION/ \
            cassandra-$VERSION | gzip > ../cassandra_$VERSION.orig.tar.gz

### Build a Debian package

    $ dpkg-buildpackage -rfakeroot -us -uc -i'\.git\/.*'
