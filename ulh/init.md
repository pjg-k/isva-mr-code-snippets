# Initializing the UserLookupHelper

The `UserLookupHelper` in IBM Security Verify Access (ISVA) offers various initialization methods to suit different configuration scenarios and requirements. Below, you'll find examples of the most common initialization uses cases.

## Using the ISVA RTE

This option utilizes the LDAP information from the ISVA Runtime Environment (RTE). To employ this configuration method, ensure that the `[bind-credentials]` stanza is populated in the `ldap.conf` configuration file. If basic user support is enabled, federated directories will be used.

```javascript
// Initialize UserLookupHelper using ISVA RTE
var ulh = new UserLookupHelper();
ulh.init(); // The default configuration will be used from the ISVA RTE
```

Alternatively, you can set the `useAuthService` parameter to `false`.

```javascript
// Initialize UserLookupHelper using ISVA RTE
var ulh = new UserLookupHelper();
ulh.init(false); // The default configuration will be used from the ISVA RTE
```

## Using the Username & Password Authentication Mechanism

The Username Password mechanism contains configurations for connecting to an LDAP, which can also be utilized by this lookup utility. Depending on the module configuration, federated directories can be utilized with this method. For detailed instructions on how to configure this mechanism, please refer to the following documentation: [Configuring Username Password Mechanism](https://www.ibm.com/docs/en/sva/10.0.6?topic=authentication-configuring-username-password).

```javascript
// Initialize UserLookupHelper using ISVA RTE
var ulh = new UserLookupHelper();
ulh.init(true); // The default configuration will be used from the ISVA RTE
```

## Using a LDAP Server Connection

You can use a server connection to initialize the `UserLookupHelper`. The server connection can be retrieved using the `ServerConnectionFactory` class. Please note that this configuration does not support basic users or federated directories.

For information on how to configure the server connection, refer to the following documentation: [Configuring Server Connections](https://www.ibm.com/docs/en/sva/10.0.6?topic=settings-server-connections).

```javascript
var ulh = new UserLookupHelper();
var ldapConnection = ServerConnectionFactory.getLdapConnectionByName(ldapConnectionName);
ulh.init(ldapConnection, 'Default');
```

### Ensure Login Failure persistence

When you need to persist login failures in the LDAP while using an LDAP server connection for initialization, you can utilize the `method. This method requires a search filter. The default search filter is`(|(objectClass=ePerson)(objectClass=Person))`.

```javascript
var ulh = new UserLookupHelper();
var ldapConnection = ServerConnectionFactory.getLdapConnectionByName(ldapConnectionName);

// Initialize the UserLookupHelper with persistent login failures handling
ulh.init(ldapConnection, '(|(objectClass=ePerson)(objectClass=Person))', 'Default', true);
```

## Providing Parameters directly

You can also specify all the connection data directly. **It's important to be aware that this approach necessitates storing the password in plain text, which may have security implications.**

```javascript
var ulh = a new UserLookupHelper();
ulh.init("ldap.example.com", 389, "cn=admin,dc=example,dc=com", "password", "Default", 5000);
```

## Additional Initialization Methods

There are more initialization methods available with various configurations, including TLS, custom search filters, client certificate authentication, and persistence settings. Refer to the JavaDoc for the UserLookupHelper class for details on these methods and their use cases.
