# All you have to know about setting up Atlas WebAPI.

1. Follow the instruction in https://github.com/OHDSI/Broadsea
2. Make necessary change in `source_source_daimon.sql` (check update in webapi doc https://github.com/OHDSI/Broadsea/tree/master/sqlserver)
3. Put `Cong_scratch` before ohdsi. `pring.jpa.properties.hibernate.default_schema=Cong_scratch.ohdsi`. Otherwise it will cause troubles.
4. Move results.\* tables to `Cong_scratch` and change schema to `results` to `ohdsi`.
5. Docker will manipulate iptables. So change the yml file.https://docs.docker.com/compose/compose-file/#ports add 127.0.0.1 to restrict the port binding.
```
broadsea-webtools:
    image: ohdsi/broadsea-webtools
    ports:
      - "127.0.0.1:8080:8080"
    volumes:
     - .:/tmp/drivers/:ro
     - ./config-local.js:/usr/local/tomcat/webapps/atlas/js/config-local.js:ro
```
6. turn on security by following http://www.ohdsi.org/web/wiki/doku.php?id=documentation:software:webapi:basic\_security
```
define([], function () {
        var configLocal = {};

        // clearing local storage otherwise source cache will obscure the override settings
        localStorage.clear();

        // WebAPI
        configLocal.api = {
                name: 'Cong_scratch',
                url: 'http://localhost:8080/WebAPI/'
        };

        configLocal.cohortComparisonResultsEnabled = false;
        configLocal.userAuthenticationEnabled = true;
        configLocal.plpResultsEnabled = false;
        configLocal.authProviders = [{
                "name": "Local Security Test DB",
                "url": "user/login/db",
                "ajax": true,
                "icon": "fa fa-database",
                "isUseCredentialsForm": true
        }];
        return configLocal;
});
```
