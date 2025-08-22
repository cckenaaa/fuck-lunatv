# fuck-lunatv

## docker-compose.yml

```yaml
services:
  fuck-lunatv:
    image: ghcr.io/moontechlab/lunatv:latest
    volumes:
      - ./hooks:/hooks:ro
    environment:
      NODE_OPTIONS: "--require /hooks/exit-hook.js"
      USERNAME: "admin"
      PASSWORD: "admin123456"
      NEXT_PUBLIC_STORAGE_TYPE: kvrocks
      KVROCKS_URL: redis://moontv-kvrocks:6666
    ports:
      - "3000:3000"
    networks:
      - moontv-network
    depends_on:
      - moontv-kvrocks
  moontv-kvrocks:
    image: apache/kvrocks
    container_name: moontv-kvrocks
    restart: unless-stopped
    volumes:
      - kvrocks-data:/var/lib/kvrocks
    networks:
      - moontv-network
networks:
  moontv-network:
    driver: bridge
volumes:
  kvrocks-data:
```

**Don't add the fucking `AUTH_TOKEN`.**
