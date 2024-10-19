# [Implement continuous delivery with Gemini](https://www.cloudskillsboost.google/course_templates/882/labs/476337)

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell

```
export ZONE=
```
```
export REGION=${ZONE%-*}
PROJECT_ID=$(gcloud config get-value project)
echo "PROJECT_ID=${PROJECT_ID}"
echo "REGION=${REGION}"

USER=$(gcloud config get-value account 2> /dev/null)
echo "USER=${USER}"

gcloud services enable cloudaicompanion.googleapis.com --project ${PROJECT_ID}

gcloud projects add-iam-policy-binding ${PROJECT_ID} --member user:${USER} --role=roles/cloudaicompanion.user
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member user:${USER} --role=roles/serviceusage.serviceUsageViewer

gcloud services enable container.googleapis.com --project ${PROJECT_ID}

gcloud projects add-iam-policy-binding ${PROJECT_ID} --member user:${USER} --role=roles/container.admin

gcloud container clusters create test \
    --project=$DEVSHELL_PROJECT_ID \
    --zone=$ZONE \
    --num-nodes=3 \
    --machine-type=e2-standard-4

git clone --depth=1 https://github.com/GoogleCloudPlatform/microservices-demo

cd ~/microservices-demo
kubectl apply -f ./release/kubernetes-manifests.yaml

sleep 120

kubectl get deployments

echo "http://$(kubectl get service frontend-external -o=jsonpath='{.status.loadBalancer.ingress[0].ip}')"

gcloud builds worker-pools create pool-test \
  --project=$DEVSHELL_PROJECT_ID \
  --region=$REGION \
  --no-public-egress

gcloud artifacts repositories create my-repo \
  --repository-format=docker \
  --location=$REGION \
  --description="My private Docker repository"
```

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
