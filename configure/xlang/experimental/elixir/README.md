# Elixir language server

This folder contains the deployment files for the Elixir language server.

🚨 **Warning**: This language server is experimental. Please [read about the caveats](https://about.sourcegraph.com/docs/code-intelligence/experimental-language-servers/#caveats-of-experimental-language-servers) before enabling it. 🚨

You can enable it by:

1. Apply the deployment files to your cluster.

   ```bash
   kubectl apply -f configure/experimental/elixir --recursive
   ```

2. Adding the following environment variables to the `lsp-proxy` deployment to make it aware of the Elixir language server's existence.

   ```yaml
   # base/lsp-proxy/lsp-proxy.Deployment.yaml
   env:
     - name: LANGSERVER_ELIXIR
       value: tcp://xlang-elixir:8080
   ```

3. `kubectl apply` your changes so that the `lsp-proxy` deployment sees the new environment variables.

   ```bash
   kubectl apply --prune -l deploy=sourcegraph -f base --recursive
   ```