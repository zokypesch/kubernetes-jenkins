gcloud container clusters create belajar-ci --zone asia-east1-a

gcloud compute disks create --size=10GB --zone=asia-east1-a jenkins-volume

kubectl apply -f manifests/

kubectl get pod,pvc,service,pv,deployment,endpoints

remove

gcloud compute disks delete jenkins-volume --zone asia-east1-a

gcloud container clusters delete belajar-ci --zone asia-east1-a

kubectl delete pod,pvc,service,pv,deployment jenkins

ok