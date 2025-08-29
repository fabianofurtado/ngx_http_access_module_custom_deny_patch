# ngx_http_access_module Custom Deny Patch

This is a small patch for the NGINX `ngx_http_access_module` that extends the functionality of the `deny` directive. It allows specifying a custom HTTP status code as a second parameter, instead of always returning the default `403 Forbidden`.

---

## 🔧 What This Patch Does

By default, the `deny` directive returns HTTP status code **403 (Forbidden)**. This patch enables the directive to optionally return **404 (Not Found)** or other codes (with minor modifications to the source code).

### ✅ Example Usage (After Patch)

```nginx
location /private/ {
    deny all 404;
}
```
In this example, requests to `/private/` will be denied with a `404 Not Found` instead of `403`.

---

## ⚙️ Supported Status Codes

Currently, the patch supports:

- `403` (`NGX_HTTP_FORBIDDEN`)
- `404` (`NGX_HTTP_NOT_FOUND`)

Support for additional status codes can be added easily.

---

## 🛠️ How to Apply the Patch

Download the NGINX source code, extract and patch:

```bash
wget https://nginx.org/download/nginx-1.29.1.tar.gz
tar -xf nginx-1.29.1.tar.gz
patch -d nginx-1.29.1/ -Np0 < ngx_http_access_module.c.patch
```
Your NGINX code is now patched! Compile it and enjoy!