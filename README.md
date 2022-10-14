## Google Cloud Maketplace Scripts for Gaming Solutions

This repo contains helpful scripts that can be used when integrating with the Google Cloud Marketplace, specifically for Gaming Solutions.

---

### Process

1. Define your configs

    ```bash
    # Copy default config file (config.default)
    cp config.default config
    
    # Edit the newly created config file by adding your own config values
    vi config
    ```

2. Setup a Cloud Function listener to receive PubSub Push messages. Note: This listener could also be deployed on Cloud Run, GKE, etc.


3. Create a Push (or Pull) PubSub subscription to the Marketplace topic called "cloudcommerceproc-prod".

```bash
GCP_PROJECT_ID=""
SERVICE_ACCOUNT_NAME=""
HTTP_ENDPOINT="" # HTTP Endpoint, I deployed via Cloud Functions
MARKETPLACE_TOPIC_NAME="" # Found in Marketplace Portal
MARKETPLACE_GCP_PROJECT_ID="cloudcommerceproc-prod" # Found in Marketplace Portal

# Create a Service Account that'll interact with the Google Marketplace
gcloud iam service-accounts create $SERVICE_ACCOUNT_NAME \
    --description="Google Marketplace Service Account" \
    --display-name=$SERVICE_ACCOUNT_NAME

# Grant the servcie account the following roles:
- Cloud Functions Invoker
- PubSub Editor
- Cloud Datastore User

# Impersonate the service account
gcloud config set auth/impersonate_service_account "$SERVICE_ACCOUNT_NAME@$GCP_PROJECT_ID.iam.gserviceaccount.com"

# Create the PubSub Subscription
gcloud pubsub subscriptions create marketplaceEventListener \
--topic=$MARKETPLACE_TOPIC_NAME \
--topic-project=cloudcommerceproc-prod \
--push-endpoint=$HTTP_ENDPOINT \
--expiration-period=never
```
