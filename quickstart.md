# Quickstart 

## Setup

1. In the Google Cloud console, on the project selector page, select or [create] a Google Cloud project. 
   Then, set the `PROJECT_ID` environment variable.

   ```shell
   export PROJECT_ID=<your-project-id>
   ``` 
   
2. Make sure that billing is [enabled][billing] for your Google Cloud project.
   
3. Enable the Vertex AI, Artifact Registry, Cloud Build, Cloud Deploy and Cloud Storage APIs.
   
    ```shell
    gcloud services enable \
      aiplatform.googleapis.com \
      artifactregistry.googleapis.com \
      compute.googleapis.com \
      cloudbuild.googleapis.com \
      clouddeploy.googleapis.com 
    ```

4. [Install][gcloud] the Google Cloud CLI.

5. [Initialize][init] the gcloud CLI.
   
   ```shell
   gcloud init
   ```

7. Make sure the default Compute Engine [service account][sa] has sufficient permissions.
   
    1. Add the `iam.serviceAccountUser` role, which includes the `actAs` permission to deploy to the runtime.
    
        ```shell
        gcloud iam service-accounts add-iam-policy-binding $(gcloud projects describe $PROJECT_ID) \
        --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
        --member=serviceAccount:$(gcloud projects describe $PROJECT_ID \
        --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
        --role="roles/iam.serviceAccountUser" \
        --project=$PROJECT_ID
        ```

    2. Add the `clouddeploy.jobRunner` role.
   
        ```shell
        gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member=serviceAccount:$(gcloud projects describe $PROJECT_ID) \
        --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
        --role="roles/clouddeploy.jobRunner"
        ```

    3. Add the `roles/clouddeploy.viewer` role.
   
        ```shell
        gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member=serviceAccount:$(gcloud projects describe $PROJECT_ID) \
        --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
        --role="roles/clouddeploy.viewer"
        ```

    4. Add the `roles/aiplatform.user` role.
   
        ```shell
        gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member=serviceAccount:$(gcloud projects describe $PROJECT_ID) \
        --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
        --role="roles/aiplatform.user"
        ```

    5. Add the `roles/storage.objectCreator` role.
   
        ```shell
        gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member=serviceAccount:$(gcloud projects describe $PROJECT_ID) \
        --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
        --role="roles/storage.objectCreator"
        ```

    6. Add the `roles/storage.objectViewer` role.
   
        ```shell
        gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member=serviceAccount:$(gcloud projects describe $PROJECT_ID) \
        --format="value(projectNumber)")-compute@developer.gserviceaccount.com \
        --role="roles/storage.objectViewer"
        ```
## Storage

1. Create a Cloud Storage bucket.
   
    ```shell
    echo "foo"
    ```

2. Create an Artifact Registry repository.
   
    ```shell
    echo "foo"
    ```

[create]: https://cloud.google.com/resource-manager/docs/creating-managing-projects
[billing]: https://cloud.google.com/billing/docs/how-to/verify-billing-enabled#console
[gcloud]: https://cloud.google.com/sdk/docs/install
[init]: https://cloud.google.com/sdk/docs/initializing
[sa]: https://cloud.google.com/iam/docs/service-account-types#default
