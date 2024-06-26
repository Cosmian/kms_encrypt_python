# kms_encrypt_python

Example of using Python to perform encryption and decryption using the
Cosmian KMS.

This project demonstrates

- the creation of a 4096-bit RSA key pair
- the encryption and decryption of a single message (using CKM_RSA_AES_KEY_WRAP)
- the encryption and decryption of multiple messages in a single request (bulk/batch feature of KMIP)

## Running the tests

1. Start a KMS Server

... using Docker

```shell
docker run -p 9998:9998 --name kms ghcr.io/cosmian/kms:4.16.0
```

... or running one of the binaries available in [https://package.cosmian.com](https://package.cosmian.com/kms/last_build/)

2. Run the tests in `tests/test_api.py` to see the examples in action.

## Developing more KMIP calls

Follow the documentation at https://docs.cosmian.com/cosmian_key_management_system/kmip_2_1/json_ttlv_api/


## Authenticating to the server

Check [this documentation](https://docs.cosmian.com/cosmian_key_management_system/authentication/).

This project demonstrates using OAuth2/OIDC to authenticate to the KMS server optionally.

URL and authentication information is loaded from the configuration file `~/.cosmian/kms.json`:
A typical file looks like this:

```json
{
    "kms_server_url": "https://kms.acme.com",
    "kms_access_token": "eyJhbGciOiJSUz..MDI3NGJiZWE2MmRhMmE4YzRhMTIiLCJ0eXAiOiJ",
    "oauth2_conf": {
        "client_id": "99673...auth.com",
        "client_secret": "GOCSPX...1M",
        "authorize_url": "https:/auth.com/auth",
        "token_url": "https://auth.com/token",
        "scopes": [
            "abc",
            "def"
        ]
    }
}
```

Use `ckms login` to get a token.

## Build the python module

Install [`tox`](https://pyscaffold.org/en/stable/features.html#configuration-packaging-distribution) and use
`tox -e build`.
