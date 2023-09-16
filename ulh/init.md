# Initializing the UserLookupHelper

#TODO: !! Add package imports to code.

The `UserLookupHelper` in IBM Security Verify Access (ISVA) offers various initialization methods to suit different configuration scenarios and requirements. Below, you'll find a description of each initialization method along with its intended use cases.

## Initialization Methods

### 1. `init()`

This initializer uses the configuration of the current appliance's Verify Access RTE. It's suitable for cases where you want to rely on the default configuration settings of the ISVA environment.

```javascript
var userLookup = new UserLookupHelper();
userLookup.init();
```

### 2. `init(boolean useAuthService)`

Initialize a `UserLookupHelper` using either the configuration in the Verify Access RTE or the configuration in the Username Password authentication mechanism. Use this when you need to choose between two different configurations based on a condition.

```javascript
var userLookup = new UserLookupHelper();
userLookup.init(true); // Use the authentication service configuration
```

### 3. `init(boolean useAuthService, java.util.Properties overrideProperties)`

Similar to the previous method, but allows you to override specific properties using a `java.util.Properties` object. This can be useful for fine-tuning the configuration.

```javascript
var userLookup = new UserLookupHelper();
var customProperties = new java.util.Properties();
// Add custom properties as needed
userLookup.init(true, customProperties); // Use the authentication service configuration with custom overrides
```

### 4. `init(LdapServerConnection connection, String mgmtDomain)`

Initialize the lookup with a server connection and management domain. Use this method when you have a specific LDAP server connection to use.

```javascript
var userLookup = new UserLookupHelper();
var ldapConnection = ServerConnectionFactory.getLdapConnectionByName(ldapConnectionName);
userLookup.init(ldapConnection, 'Default');
```

### 5. `init(LdapServerConnection connection, String searchFilter, String mgmtDomain, boolean loginFailuresPersistent)`

Initialize the lookup with a server connection, a custom search filter, and a management domain and handle login failures persistently.

```javascript
var userLookup = new UserLookupHelper();
var ldapConnection = ServerConnectionFactory.getLdapConnectionByName(ldapConnectionName);

// Initialize the UserLookupHelper with persistent login failures handling
userLookup.init(ldapConnection, '(&(objectclass=person))', 'Default', true);
```

### 6. `init(String hostname, int port, String bindDn, String bindDnPwd, String mgmtDomain, int connectionTimeout)`

Basic initialization with server connection details, management domain, and connection timeout settings. This method is suitable for straightforward LDAP configurations.

```javascript
var userLookup = a new UserLookupHelper();
userLookup.init("ldap.example.com", 389, "cn=admin,dc=example,dc=com", "password", "Default", 5000);
```

### Additional Initialization Methods

There are more initialization methods available with various configurations, including TLS, custom search filters, client certificate authentication, and persistence settings. Refer to the JavaDoc for the `UserLookupHelper` class for details on these methods and their use cases.

## Conclusion

Select the appropriate initialization method for your specific IBM Security Verify Access mapping rules and LDAP configuration needs. These methods allow you to tailor the `UserLookupHelper` to your requirements and make informed authentication and authorization decisions within your ISVA environment.
