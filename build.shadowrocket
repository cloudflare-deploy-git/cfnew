#!/bin/bash
cp "少年你相信光吗" index.js

KVID=$(npx wrangler kv namespace list | jq -r '.[] | select(.title | contains("cfnew")) | .id' | head -n 1)

if [ -z "$KVID" ] || [ "$KVID" = "null" ]; then
  KVID=$(npx wrangler kv namespace create cfnew 2>&1 | grep -oE '[a-f0-9]{32}' | head -n 1)
fi

printf 'name = "cfnew"\nmain = "index.js"\ncompatibility_date = "2026-09-03"\n\nroutes = [\n  { pattern = "cfnew.sophieweb.ccwu.cc", custom_domain = true }\n]\n\n[vars]\nu = "G20180531"\n\n[[kv_namespaces]]\nbinding = "C"\nid = "%s"\n' "$KVID" > wrangler.toml
