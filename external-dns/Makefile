NAMESPACE=externaldns
DOMAIN_FILTER=exchangeweb.net
AWS_ZONE_TYPE=public
REGISTRY=txt
TXT_OWNER_ID=external-dns
ARN=aws-assume-role=arn:aws:iam::401413892014:role/R53-Records-Management
REGION=us-east-1

ns:
	kubectl create namespace $(NAMESPACE)

dns:
	sed -i '' 's/externaldns/$(NAMESPACE)/g' external-dns-rbac.yaml
	sed -i '' 's/--domain-filter=$$(DOMAIN_FILTER)/--domain-filter=$(DOMAIN_FILTER)/g' external-dns-rbac.yaml
	sed -i '' 's/--aws-zone-type=public/--aws-zone-type=$(AWS_ZONE_TYPE)/g' external-dns-rbac.yaml
	sed -i '' 's/--registry=txt/--registry=$(REGISTRY)/g' external-dns-rbac.yaml
	sed -i '' 's/--txt-owner-id=\$$(TXT_OWNER_ID)/--txt-owner-id=$(TXT_OWNER_ID)/g' external-dns-rbac.yaml
	sed -i '' 's#--aws-assume-role=arn:aws:iam::YOUR_ACCOUNT_ID:role/YOUR_ROLE_NAME#--$(ARN)#g' external-dns-rbac.yaml
	sed -i '' 's/AWS_REGION: "us-east-1"/AWS_REGION: "$(REGION)"/g' external-dns-rbac.yaml
	kubectl apply -f external-dns-rbac.yaml

stop:
	kubectl delete -f external-dns-rbac.yaml

destroy:
	kubectl delete namespace $(NAMESPACE)
