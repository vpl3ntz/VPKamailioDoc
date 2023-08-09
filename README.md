<pre><code>  _  __                              _   _   _         
 | |/ /   __ _   _ __ ___     __ _  (_) | | (_)   ___  
 | ' /   / _` | | '_ ` _ \   / _` | | | | | | |  / _ \ 
 | . \  | (_| | | | | | | | | (_| | | | | | | | | (_) |
 |_|\_\  \__,_| |_| |_| |_|  \__,_| |_| |_| |_|  \___/ 
                                                       </code></pre>

# Kamailio Document [5.3.x] | <a href="https://kamailio.org/docs/modules/5.3.x/">Documentation</a>

- Este projeto, pretende listar os módulos utilizados em produção, juntamente com a documentação e como implementar.
# [Postgres](https://www.kamailio.org/docs/modules/devel/modules/db_postgres.html#idm22)
**Como implementar PostgreSQL:**

*Definir no inicio*
<pre><code>!define WITH_PGSQL</code></pre>

*Defined Values*
<pre><code>#!ifdef WITH_PGSQL
#!ifndef DBURL
#!define DBURL "postgres://username:password@localhost:port/dbname"
#!endif</code></pre>

*Modules section*
<pre><code>#!ifdef WITH_PGSQL
loadmodule "db_postgres.so"
#!endif</code></pre>

# [Redis](https://kamailio.org/docs/modules/5.3.x/modules/db_redis.html)
**Como implementar Redis:**

*Definir no inicio*
<pre><code>!define WITH_REDIS</code></pre>

*Defined Values*
<pre><code>#!ifdef WITH_REDIS
loadmodule "ndb_redis.so"
modparam("ndb_redis", "server", "name=tcp;addr=localhost;port=port")
#!endif</code></pre>

# [Auth](https://kamailio.org/docs/modules/5.3.x/modules/auth.html)
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
modparam("auth_db", "use_domain", MULTIDOMAIN)
!#endif</code></pre>

# [IPAuth](https://kamailio.org/docs/modules/5.3.x/modules/permissions.html)
**Como implementar IPAuth:**

*Definir no inicio*
<pre><code>#!define WITH_IPAUTH</code></pre>

*Defined Values*
<pre><code>#!ifndef DBURL
#!define DBURL "postgres://kamailio:password@localhost:port/kamailio"
#!endif</code></pre>

*Modules section*
<pre><code>#!ifdef WITH_IPAUTH
loadmodule "permissions.so"
#!endif</code></pre>

*Setting module-specific parameters*
<pre><code>#!ifdef WITH_IPAUTH
modparam("permissions", "db_url", DBURL)
modparam("permissions", "db_mode", 1)
#!endif</code></pre>

# [Usrlocdb](https://kamailio.org/docs/modules/5.2.x/modules/usrloc.html#idm46)
**Como implementar Usrlocdb:**

*Definir no inicio*
<pre><code>#!define WITH_USRLOCDB</code></pre>

*Defined Values*
<pre><code>#!ifndef DBURL
#!define DBURL "postgres://kamailio:password@localhost:port/kamailio"
#!endif</code></pre>

*Setting module-specific parameters*
<pre><code>
modparam("usrloc", "preload", "location")
#!ifdef WITH_USRLOCDB
modparam("usrloc", "db_mode", 2)
modparam("usrloc", "use_domain", MULTIDOMAIN)
#!endif</code></pre>

# [SQLOps](https://kamailio.org/docs/modules/5.3.x/modules/sqlops.html#sqlops.p.sqlcon)
**Como implementar SQLOps:**

*Definir no inicio*
<pre><code>#!define WITH_SQLOPS</code></pre>

*Modules section*
<pre><code>!ifdef WITH_SQLOPS
loadmodule "sqlops.so"
modparam("sqlops","sqlcon","alias=>postgres://username:password@localhost:port/dbname")
#!endif
</code></pre>

# [Counters](https://kamailio.org/docs/modules/5.3.x/modules/counters.html)
**Como implementar Counters:**

*Definir no inicio*
<pre><code>#!define WITH_COUNTERS</code></pre>

*Modules section*
<pre><code>#!ifdef WITH_COUNTERS
loadmodule "counters.so"
modparam("counters", "script_counter", "execute example")
#!endif</code></pre>

# [Statistics](https://kamailio.org/docs/modules/5.3.x/modules/statistics.html)
**Comom implmentar Statistics:**

*Definir no inicio*
<pre><code>#!define WITH_STATISTICS</code></pre>

*Modules section*
<pre><code>#!ifdef WITH_STATISTICS
loadmodule "statistics.so"
modparam("statistics", "variable", "name of statistic")
#!endif</code></pre>

# [Uac(User Agent Client)](https://kamailio.org/docs/modules/5.3.x/modules/uac.html)
**Como implementar Uac:**

*Definir no inicio*
<pre><code>#!define WITH_UAC</code></pre>

*Module sections*
<pre><code>#!ifdef WITH_UAC
loadmodule "uac.so"
modparam("uac", "reg_db_url", "postgres://username:password@localhost:port/dbname")
modparam("uac", "reg_contact_addr", "localhost")
modparam("uac","restore_mode","manual")
#!endif</code></pre>

# [Cfgutils](https://kamailio.org/docs/modules/5.3.x/modules/cfgutils.html)
**Como implementar Cfgutils:**

*Definir no inicio*
<pre><code>#!define WITH_CFGUTILS</code></pre>

*Modules section*
<pre><code>#!ifdef WITH_CFGUTILS
loadmodule "cfgutils.so"
modparam("cfgutils", "hash_file", "DIRECTORY/kamailio.cfg")
modparam("cfgutils", "initial_probability", 15)
modparam("cfgutils", "initial_gflags", 15)
modparam("cfgutils", "lock_set_size", 4)
#!endif</code></pre>

**Extra:**

- [Modules parameters](https://www.kamailio.org/wiki/alphaindexes/5.3.x/modparameters?s[]=postgres)