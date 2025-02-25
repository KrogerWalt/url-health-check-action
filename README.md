# URL health check action

A cURL-based post-deploy health check with build-in redirect & retry. A quick & easy way to verify a deployment.   

```yaml
steps:
  - name: Check the deployed service URL
    uses: KrogerWalt/url-health-check-action@main
    with:
      # Check the following URLs one by one sequentially
      url: https://example.com|http://example.com
      # Follow redirects, or just report success on 3xx status codes
      follow-redirect: false # Optional, defaults to "false"
      # Fail this action after this many failed attempts
      max-attempts: 3 # Optional, defaults to 1
      # Delay between retries
      retry-delay: 5s # Optional, only applicable to max-attempts > 1
      # Retry all errors, including 404. This option might trigger curl upgrade.
      retry-all: false # Optional, defaults to "false"
      # Tell curl to skip certificate validation when making the call
      skip-validation: false # Optional, defaults to "false"
```

The action will fail if any of the URLs reports either 4xx or 5xx status codes.
