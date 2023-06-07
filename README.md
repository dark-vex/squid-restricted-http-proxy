# Squid Restricted HTTP Proxy

Squid proxy for restricting external HTTP access.

This is designed for internal use by Kubernetes applications, and includes a service but not an ingress.

## Example usage

    git clone https://github.com/dark-vex/squid-restricted-http-proxy.git && cd squid-restricted-http-proxy

    helm upgrade --install squid . --namespace squid --create-namespace=squid

    # Start an interactive shell
    kubectl run my-shell --rm -i --tty --image=nginx --restart=Never \
    --env=http_proxy=http://squid-squid-restricted-http-proxy.squid:3128 \
    --env=https_proxy=http://squid-squid-restricted-http-proxy.squid:3128 \
    sh

    # This HEAD request should work
    curl -I https://www.openmicroscopy.org

    # This HEAD request should fail
    curl -I https://www.dundee.ac.uk
