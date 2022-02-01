## Google Cloud Maketplace Scripts for Gaming Solutions

This repo contains helpful scripts that can be used when integrating with the Google Cloud Marketplace, specifically for Gaming Solutions.

---
### Process

1. Define your configs

```
# Copy default config file (config.default)
cp config.default config

# Edit the newly created config file by adding your own config values
vi config
```

2. Setup a Cloud Function listener to receive PubSub Push messages. Note: This listener could also be deployed on Cloud Run, GKE, etc.


3. Create a Push (or Pull) PubSub subscription to the Marketplace topic called "cloudcommerceproc-prod".

