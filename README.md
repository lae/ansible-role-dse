lae.dse
=========

Role for installing and configuring Datastax Enterprise.

Role Variables
--------------

TBD (the following is possibly archaic and needs updates/features reimplemented)

|Name|Type|Description|Default|
|----|----|-----------|-------|
|dse_type|String|Usable values are hadoop, search, spark, and searchanalytics. Anything else will configure a server to be a standard Cassandra node.|cassandra|
|dse_repo|String|DSE repo location, most likely with your DSE credentials - can point to a mirror however| https://dsa_email_address:password@debian.datastax.com/enterprise|
|dse_repo_key_id|String|Fingerprint of your DSE repo's packaging key, useful if you sign your own packages on your mirror, otherwise keep the original DSE key|B999A372|
|dse_repo_key_url|String|URL where your DSE repo's packaging key can be found|https://debian.datastax.com/debian/repo_key|
|dse_auditlog_enabled|Boolean|Whether or not to enable the audit log.|false|
|dse_install_pig|Boolean|Whether or not to install Apache Pig.|false|
|dse_cassandra_max_heap_size|String|Amount of memory dedicated to the Java heap (set together with heap_newsize). Dynamically defined if left unset.|undefined|
|dse_cassandra_heap_newsize|String|Size of the young generation (set together with max_heap_size). Dynamically defined if left unset.|undefined|
|dse_cassandra_jmx_port|String|Port for Cassandra's JMX (metrics) to listen on.|7199|
|dse_cassandra_jmx_password_file|String|Location of credentials file for Cassandra's JMX.|/etc/dse/cassandra/jmxremote.password|

Dependencies
------------

By default, the DSE package will pull in OpenJDK in as its Java dependency. You should install Oracle Java prior to this role if you would prefer to use it, such as with the williamyeh.oracle-java role in the examples.

Example Playbook/Inventory
----------------

`inventory`:

    [cass01]
    host02
    host03
    
    [cass01_seeds]
    host01
    
    [cass01:children]
    cass01_seeds

`playbook.yml`:

    - hosts: cass01
      become: True
      roles:
        - lae.dse

License
-------

MIT
