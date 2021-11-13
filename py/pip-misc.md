---
title: PIP Misc
nav: pip misc
---

## SSL cert failure

The most common issue to install a package in a company network is

```text
 SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:581)
```
this is because the company network blocks the access for various reasons such as security concerns.

To overwrite that, you need to specify ``trusted-host`` by observing the source host from pip output.

The most common pip source hosts are
* pypi.org
* files.pythonhosted.org

So following command resolves most of the problems
```bash
sudo pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org debugpy
```
* [debugpy](https://github.com/microsoft/debugpy/) is a debugger that implements the Debug Adapter Protocol: debugProtocol.json, you should replace it with your package name.

ref
* [ssl certificate failed](https://www.listendata.com/2019/04/connection-error-ssl-certificate-failed.html)

