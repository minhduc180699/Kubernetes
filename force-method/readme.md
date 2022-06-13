Force kill ns:
kubectl proxy &
kubectl get namespace ds-ns-rm-qa -o json |jq '.spec = {"finalizers":[]}' >temp.json
curl -k -H "Content-Type: application/json" -X PUT --data-binary @temp.json 127.0.0.1:8001/api/v1/namespaces/ds-ns-rm-qa/finalize

DELETE ALL BY STATUS:
kubectl get pod -n monitoring | grep Evicted | awk '{print $1}' | xargs kubectl delete pod -n monitoring
kubectl get pod -n ds-ns | grep NodeAffinity | awk '{print $1}' | xargs kubectl delete pod -n ds-ns
kubectl get pod -n ds-ns-rm-recommendation | grep NodeAffinity | awk '{print $1}' | xargs kubectl delete pod -n ds-ns-rm-recommendation

CLOUD FUNCTION:
<!-- with enviroment -->
gcloud functions deploy realtime-metasearch-function --runtime=java11 --trigger-http --memory=256MB --region=us-central1 --source=. --entry-point=com.deepsignal.realtimemeatasearch.RealtimeMetasearch --timeout=300s


sb=zOtLYkvJzQWdOO6_iMz58c5o,datr=zOtLYqfDYYk9YzfMh-ICMSo6,m_pixel_ratio=1,c_user=100003912251390,fbl_st=100614980%3BT%3A27545086,fbl_cs=AhAtoufPZkAlAteuAdMKOwAEGDNSbkEzT3hQMG4xeW85Q093RDd1L1h2RQ,fbl_ci=571861600965057,wd=1278x923,usida=eyJ2ZXIiOjEsImlkIjoiQXJjOGdsNzE5M3pkb3AiLCJ0aW1lIjoxNjUzMTM2ODk0fQ%3D%3D,xs=21%3AxaPwSrnmH8LMEA%3A2%3A1652323280%3A-1%3A6335%3A%3AAcXmrygANysFPB60ugElz6yLvGiYR1xJkDAj4rV_kMA,fr=0X3tkPBHDxVDMB8z9.AWUm75QE7O-Cf2u6gaNblmUSs0o.BikDbM.Wp.AAA.0.0.BikDwx.AWVa-OMpbLU,presence=C%7B%22t3%22%3A%5B%7B%22i%22%3A%22u.100009353318761%22%7D%2C%7B%22i%22%3A%22u.100009912094503%22%7D%2C%7B%22i%22%3A%22u.100021364463226%22%7D%2C%7B%22i%22%3A%22g.1613046028911683%22%7D%2C%7B%22i%22%3A%22u.1127082500679323%22%7D%2C%7B%22i%22%3A%22u.100005690624737%22%7D%2C%7B%22i%22%3A%22u.100005917652025%22%7D%2C%7B%22i%22%3A%22u.100004196863764%22%7D%2C%7B%22i%22%3A%22u.100008720221641%22%7D%2C%7B%22i%22%3A%22g.4761345440609279%22%7D%2C%7B%22i%22%3A%22g.3433429230115302%22%7D%2C%7B%22i%22%3A%22u.100005278861478%22%7D%2C%7B%22i%22%3A%22u.100010938917638%22%7D%2C%7B%22i%22%3A%22u.100002964462680%22%7D%2C%7B%22i%22%3A%22u.1646898408891409%22%7D%2C%7B%22i%22%3A%22u.100025898640813%22%7D%2C%7B%22i%22%3A%22g.4993412750713743%22%7D%2C%7B%22i%22%3A%22u.100030394151664%22%7D%5D%2C%22utc3%22%3A1653619772601%2C%22lm3%22%3A%22u.100003912251390%22%2C%22v%22%3A1%7D