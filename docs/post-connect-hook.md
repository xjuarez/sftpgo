# Post connect hook

This hook is executed as soon as a new connection is estabilished. It notifies the connection's IP address and protocol. Based on the received response, the connection is accepted or rejected. This way you can implement your own blacklist/whitelist of IP addresses.
Please keep in mind that you can easily configure specialized program such as [Fail2ban](http://www.fail2ban.org/) for brute force protection.

The `post_connect_hook` can be defined as the absolute path of your program or an HTTP URL.

If the hook defines an external program it can reads the following environment variables:

- `SFTPGO_CONNECTION_IP`
- `SFTPGO_CONNECTION_PROTOCOL`

If the external command completes with a zero exit status the connection will be accepted otherwise rejected.

Previous global environment variables aren't cleared when the script is called.
The program must finish within 20 seconds.

If the hook defines an HTTP URL then this URL will be invoked as HTTP GET with the following query parameters:

- `ip`
- `protocol`

The connection is accepted if the HTTP response code is `200` otherwise rejeted.

The HTTP request will use the global configuration for HTTP clients.