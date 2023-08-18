# Custom Endpoint URLs

The sandbox and production base URLs are defined as part of the proxy configuration, but since the wildcard domains for systems differs, they are not copied or exported when performing the actions described in this demo.  However, it is a simple command that can be run when the API Product is first imported to update these values.

The command syntax is `3scale proxy update <remote> <service-name|id> [-p param=value]`

Multiple parameters can be passed as separate -p arguments in the same command.

There are many parameters of the proxy which can be updated by this command, however the two we need to focus on are `endpoint` for the production public base url, and `sandbox_endpoint` for the sandbox public base url. The default naming scheme is "`https://<system-name>-<tenant>-apicast-<environment>.<wildcard-domain>:443`"

So in our case to update the public base URLs of the API product we have freshly imported we would execute a command similar to this, which omits the `<tenant>-apicast` from the production public base url.

~~~
$ toolbox 3scale proxy update $SOURCE weather-alerts -p endpoint=https://weather-alerts-production.apps.uscell.lab.upshift.rdu2.redhat.com:443
{
  "service_id": 3,
  "endpoint": "https://weather-alerts-production.apps.uscell.lab.upshift.rdu2.redhat.com:443",
  "api_backend": "https://api.weather.gov:443",
  "credentials_location": "query",
  "auth_app_key": "app_key",
  "auth_app_id": "app_id",
  "auth_user_key": "user_key",
  "error_auth_failed": "Authentication failed",
  "error_auth_missing": "Authentication parameters missing",
  "error_status_auth_failed": 403,
  "error_headers_auth_failed": "text/plain; charset=us-ascii",
  "error_status_auth_missing": 403,
  "error_headers_auth_missing": "text/plain; charset=us-ascii",
  "error_no_match": "No Mapping Rule matched",
  "error_status_no_match": 404,
  "error_headers_no_match": "text/plain; charset=us-ascii",
  "error_limits_exceeded": "Usage limit exceeded",
  "error_status_limits_exceeded": 429,
  "error_headers_limits_exceeded": "text/plain; charset=us-ascii",
  "secret_token": "Shared_secret_sent_from_proxy_to_API_backend_7d210c57227f993a",
  "hostname_rewrite": "",
  "sandbox_endpoint": "https://weather-alerts-3scale-apicast-staging.apps.uscell.lab.upshift.rdu2.redhat.com:443",
  "api_test_path": "/",
  "policies_config": [
    {
      "name": "default_credentials",
      "version": "builtin",
      "configuration": {
        "auth_type": "user_key",
        "user_key": "1234567890"
      },
      "enabled": false
    },
    {
      "name": "apicast",
      "version": "builtin",
      "configuration": {
      },
      "enabled": true
    },
    {
      "name": "url_rewriting",
      "version": "builtin",
      "configuration": {
        "query_args_commands": [
          {
            "value_type": "plain",
            "op": "delete",
            "arg": "user_key"
          }
        ],
        "commands": [

        ]
      },
      "enabled": true
    }
  ],
  "created_at": "2023-08-16T19:57:01Z",
  "updated_at": "2023-08-18T21:07:45Z",
  "deployment_option": "hosted",
  "lock_version": 19,
  "links": [
    {
      "rel": "mapping_rules",
      "href": "/admin/api/services/3/proxy/mapping_rules"
    },
    {
      "rel": "self",
      "href": "/admin/api/services/3/proxy"
    },
    {
      "rel": "service",
      "href": "/admin/api/services/3"
    }
  ]
}
~~~

The output of this command will be the resulting proxy configuration after the changes made by the `3scale proxy update` command, so we can verify the change.

Other possible parameters that can be overridden can be found by inspecting the built-in API docs in the gateway at the URL
https://<tenant>-admin.<wildcard-domain>/p/admin/api_docs

Search for 'Proxy Update' to see the list of parameters available.