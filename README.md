<h1>Complete CI/CD Pipeline with EKS and AWS ECR</h1>
<h6>Technologies used</h6>
apiVersion: v1
kind: Service
metadata:
  name: $APP_NAME
spec:
  selector:
    app: $APP_NAME
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
