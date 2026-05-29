# JIRA-HOSPITAL

<img width="1271" height="770" alt="image" src="https://github.com/user-attachments/assets/acf895ec-68ec-4afb-8555-cf6fc27c68e4" />

<img width="1373" height="756" alt="image" src="https://github.com/user-attachments/assets/af35bf92-2a90-4783-a283-fad8f8b48cb2" />



<img width="1389" height="765" alt="image" src="https://github.com/user-attachments/assets/e106a25d-22eb-45a4-a169-817bde0cb2c3" />

<img width="1390" height="765" alt="image" src="https://github.com/user-attachments/assets/5e3106ff-0510-4cf8-a8e9-a3bc62cb522f" />

<img width="1271" height="734" alt="image" src="https://github.com/user-attachments/assets/c7e98bd7-c054-4e45-b6a5-82509a965c99" />



# DOCKER IMPLEMENTATION

<img width="1321" height="786" alt="image" src="https://github.com/user-attachments/assets/18223a1f-d173-4542-b727-ca3772147dcb" />

<img width="1304" height="717" alt="image" src="https://github.com/user-attachments/assets/072958b2-2c94-43ff-85a4-f53939a25ba7" />


<img width="1324" height="756" alt="image" src="https://github.com/user-attachments/assets/9eeae0db-4683-4953-8114-878a1318f16c" />


<img width="1297" height="737" alt="image" src="https://github.com/user-attachments/assets/ffff0d8d-5b4f-4730-8b8a-a4a7212275a4" />

# AFTER DOCKER IMAEG PUSH NEED TO DEPLOY APP AND ADD MANGODB SOTAGE BECUSE WE ARE USING BACKEND

<img width="1383" height="238" alt="image" src="https://github.com/user-attachments/assets/82b55c7e-2922-487b-8e6e-ed335e74ce46" />
<img width="1378" height="341" alt="image" src="https://github.com/user-attachments/assets/a66952be-8f35-4ef8-8757-0c76921ca15b" />

<img width="1401" height="525" alt="image" src="https://github.com/user-attachments/assets/3080d43a-8489-4321-a284-2a1dd5151f56" />

<img width="1499" height="874" alt="image" src="https://github.com/user-attachments/assets/e9898eff-9540-450d-82bb-8012d663fe84" />











<img width="1069" height="527" alt="image" src="https://github.com/user-attachments/assets/d6855b6b-7ea1-4d0a-bee9-d54ea2c6fe69" />
<img width="1056" height="528" alt="image" src="https://github.com/user-attachments/assets/5616bdd8-e99c-492a-9396-95e3fb8ba470" />
<img width="1077" height="490" alt="image" src="https://github.com/user-attachments/assets/f28c39de-48f1-4e9a-ae93-95cc646f383c" />


<img width="1421" height="231" alt="image" src="https://github.com/user-attachments/assets/94bf455a-05a4-48f7-b7c3-2bd5bae5054c" />

Step 0 — Fix the replica count (do this first)
Open hospital-chart/values.yaml on the VM:


nano hospital-chart/values.yaml
Find replicas: 2 (under app:) and change it to:


  replicas: 1
Save (Ctrl+O, Enter, Ctrl+X). Also confirm repository: nanineelapu/hospital-app is correct there. ✅

1) Remove the plain manifests (so they don't clash with Helm)

kubectl delete -f k8s/app-deployment.yaml -f k8s/mongodb-statefulset.yaml -f k8s/config-and-secret.yaml
Note: this does not delete your storageclass — good, we keep that.

2) Validate the chart

helm lint hospital-chart
Should say 1 chart(s) linted, 0 chart(s) failed.

3) Install via Helm

helm install hospital ./hospital-chart
4) Verify

helm list
kubectl get pods
Wait for hospital-app-... and mongodb-0 to be Running.

5) Get the public URL again

kubectl get svc hospital-service
Open the EXTERNAL-IP in your browser to confirm it still works.

📸 Screenshots for the milestone:

Output of helm list (showing your hospital release)
kubectl get pods showing pods Running after the Helm install
✅ Done when: helm list shows your release and pods are Running.

➡️ Next: Step 16 — Pull Request

Run it and paste helm list + kubectl get pods. If anything errors (lint or install), send me the output and we'll fix it.

💡 Tip: if you'd rather keep replicas: 2 for the HA requirement, instead of editing the file you can override at install time: helm install hospital ./hospital-chart --set app.replicas=1 — but editing values.yaml is cleaner for grading.
