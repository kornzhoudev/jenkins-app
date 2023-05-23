# Complete CI/CD Pipeline with EKS and AWS ECR
## Technologies used
### Kubernetes, Jenkins, AWS EKS, AWS ECR, Java, Maven, Linux, Docker, Git
···
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
···
      
