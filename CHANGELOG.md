# Changelog

## 2.0.0

Fork of `diablomedia/zendframework1-http`, published as `gizmocraft/zendframework1-http`.

### Breaking changes

- Requires PHP `>=8.5`. Tested on PHP 8.5 and 8.6.
- Package renamed from `diablomedia/zendframework1-http` to `gizmocraft/zendframework1-http`. It now requires `gizmocraft/zendframework1-exception` `^2.0.0`, `gizmocraft/zendframework1-config` `^3.0.0`, `gizmocraft/zendframework1-loader` `^2.0.0`, `gizmocraft/zendframework1-date` `^2.0.0`, `gizmocraft/zendframework1-session` `^3.0.0` and `gizmocraft/zendframework1-uri` `^2.0.0`.

### Other changes

- `Zend_Http_Client_Adapter_Curl`: `getHandle()` and the `$_curl` property now document `CurlHandle|null` instead of `resource` (the type has been `CurlHandle` since PHP 8.0; no runtime change). `close()` no longer calls `curl_close()` (deprecated in PHP 8.5, no effect since PHP 8.0); the handle is released by dropping the reference.
- `Zend_Http_Client_Adapter_Curl`: a `curloptions` entry with an option number cURL does not know now raises `Zend_Http_Client_Exception` ("Unknown or erroreous cURL option") as documented. PHP 8 throws a `ValueError` there, which escaped before.
- Dev dependencies upgraded (PHPUnit 13, PHPStan 2.3, php-cs-fixer 3.95, GrumPHP 2.27). Dropped `composer-require-checker`, which has no release for PHP 8.6.
- Tests migrated to PHPUnit 13 attributes (`#[Group]`, `#[DataProvider]`, `#[DoesNotPerformAssertions]`). The dynamic client tests (socket, keepalive, persistent, proxy, cURL) were broken on PHPUnit 13 and are repaired (`getName()`, `readAttribute()`, `assertNotContains()` on strings, missing `parent::setUp()`, removed `CURLOPT_CLOSEPOLICY`). They only run when `TESTS_ZEND_HTTP_CLIENT_BASEURI` (and, for the proxy tests, `TESTS_ZEND_HTTP_CLIENT_HTTP_PROXY`) point to a web server serving `tests/Zend/Http/Client/_files`.
- Removed an obsolete PHPStan ignore for the cURL handle property.
- CI runs PHP 8.5 and 8.6.
