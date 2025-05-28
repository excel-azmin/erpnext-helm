

# make sure site name is same 

![alt text](image.png)

helm install erpnext  ./erpnext-helm -f ./erpnext-helm/values.yaml


kubectl get ingress



kubectl exec -it deploy/erpnext-gunicorn -n default -- ls /home/frappe/frappe-bench/sites


chmod -R 775 /home/frappe/frappe-bench/sites
chown -R frappe:frappe /home/frappe/frappe-bench/sites


kubectl rollout restart deployment erpnext-gunicorn
kubectl rollout restart deployment erpnext-nginx

# access mariadb 

kubectl exec -it erpnext-mariadb-0 -- bash

# access erpnext terminal 

kubectl exec -it deploy/erpnext-gunicorn -- bash

# create site 

kubectl exec -it deploy/erpnext-gunicorn -- bash
cd frappe-bench

bench new-site erp.k8s.com \
  --admin-password changeit \
  --mariadb-root-password changeit \
  --install-app erpnext


# Restart Services

kubectl rollout restart deployment erpnext-gunicorn
kubectl rollout restart deployment erpnext-nginx
