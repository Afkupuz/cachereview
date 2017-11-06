==========================
Architecture page template
==========================

Oslo.cache architecture - 1.26.1/Pike
---------------------------------------------
**Status**: Draft/Ready for Review/Reviewed

**Release**: Pike

**Version**: 1.26.1

**Contacts**:

- PTL: name - irc handle

- Architect: name - irc handle

- Security Reviewer: name - irc handle


Project description and purpose
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
oslo.cache aims to provide a generic caching mechanism for OpenStack 
projects by wrapping the dogpile.cache library. The dogpile.cache library 
provides support memorization, key value storage and interfaces to common 
caching backends such as Memcached. [0]_


Primary users and use-cases
~~~~~~~~~~~~~~~~~~~~~~~~~~~
The primary use of Oslo.cache is to abstract out any code related to
the cache, specifically for dogpile and memcache integration.


External dependencies & associated security assumptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Oslo.cache is a wrapper for dogpile and integrates with memcache.
All dependencies are already present in global requirements.
Without cached memory the service is useless.
From a security standpoint, nothing is changed beyond bringing
cache management into a single location which will make it easier
to update and track. We continue to assume that user will encrypt
keys before storage as there is no inherent security. [1]_


Components
~~~~~~~~~~

- memcache
- Memcached
	- BMemcached
	- Standard Memcached
	- Pylibmc
- In-Memory (Python dict-based)
- Redis
- MongoDB


Service architecture diagram
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: figures/keystonemiddleware_architecture-diagram.png

Architecture Page [2]_


Data assets
~~~~~~~~~~~

- Config data from Oslo.conf


Data asset impact analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~
Data Assets:
- *Cache Breach*:
  - Integrity Failure Impact: Attacker that can infiltrate cache can gain access to stored token. Tokens should be stored encrypted for maximum
  security.


Resources
~~~~~~~~~

.. [0] `<https://github.com/openstack/oslo.cache>`
.. [1] `<https://specs.openstack.org/openstack/oslo-specs/specs/kilo/oslo-cache-using-dogpile.html>`_
.. [2] `<https://docs.openstack.org/oslo.cache/latest>`
.. [3] `<https://specs.openstack.org/openstack/oslo-specs>`