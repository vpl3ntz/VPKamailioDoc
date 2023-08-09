<img src="kamailio-logo.png" width=272 alt="Kamailio">

# Kamailio Document [5.3.x] | <a href="https://kamailio.org/docs/modules/5.3.x/">Documentation</a>

# Módulos:

# [Postgres](https://www.kamailio.org/docs/modules/devel/modules/db_postgres.html#idm22)
**Como implementar PostgreSQL:**

*Definir no inicio*
<pre><code>!define WITH_PGSQL</code></pre>

*"Defined Values"*
<pre><code>#!ifdef WITH_PGSQL
#!ifndef DBURL
#!define DBURL "postgres://kamailio:password@localhost:port/kamailio"
#!endif</code></pre>

*"Modules section"*
<pre><code>#!ifdef WITH_PGSQL
loadmodule "db_postgres.so"
#!endif</code></pre>

# [Redis](https://kamailio.org/docs/modules/5.3.x/modules/db_redis.html)
**Como implementar Redis:**

*Definir no inicio*
<pre><code>!define WITH_REDIS</code></pre>

*"Defined Values"*
<pre><code>#!ifdef WITH_REDIS
loadmodule "ndb_redis.so"
modparam("ndb_redis", "server", "name=tcp;addr=localhost;port=port")
#!endif</code></pre>

- # [Auth](https://kamailio.org/docs/modules/5.3.x/modules/auth.html)
**Como implementar Auth(Back-end/Data-base):**

*Definir no inicio*
<pre><code>!#define WITH_AUTH</code></pre>

*Modules section*
<pre><code>#!ifdef WITH_AUTH
loadmodule "auth.so"
loadmodule "auth_db.so"
#!endif</code></pre>

*Setting module-specific parameters*
<pre><code>#!ifdef WITH_AUTH
modparam("auth_db", "db_url", DBURL)
modparam("auth_db", "calculate_ha1", yes)
modparam("auth_db", "password_column", "password")
modparam("auth_db", "load_credentials", "")
modparam("auth_db", "use_domain", MULTIDOMAIN)</code></pre>

**Extra:**

- [Modules parameters](https://www.kamailio.org/wiki/alphaindexes/5.3.x/modparameters?s[]=postgres)