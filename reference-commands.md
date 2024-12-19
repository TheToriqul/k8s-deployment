# Kubernetes Deployment Command Reference Guide

### Project Content Table
- [Core Deployment Operations](#core-deployment-operations)
- [Advanced Management Commands](#advanced-management-commands)
- [Monitoring and Debugging](#monitoring-and-debugging)
- [Cleanup Operations](#cleanup-operations)

> **Author**: [Md Toriqul Islam](https://linkedin.com/in/thetoriqul)  
> **Description**: Comprehensive command reference for Kubernetes Deployment management  
> **Learning Focus**: Mastering Kubernetes Deployment workflows  
> **Note**: Review and understand each command before execution in your environment.

## Core Deployment Operations

### Creating the Deployment

#### Declarative Approach
```bash
# Create deployment using YAML manifest
kubectl apply -f deployment-definition.yaml

# Verify deployment creation
kubectl get deployment nginx-deployment

# Check deployment status
kubectl rollout status deployment/nginx-deployment
```

#### Imperative Approach
```bash
# Create deployment directly via command line
kubectl create deployment nginx-deployment \
    --image=nginx:latest \
    --replicas=3 \
    --port=80

# Verify pods creation
kubectl get pods -l app=nginx
```

## Advanced Management Commands

### Scaling Operations
```bash
# Scale deployment replicas
kubectl scale deployment nginx-deployment --replicas=5

# Verify scaling operation
kubectl get pods -w

# Enable autoscaling
kubectl autoscale deployment nginx-deployment \
    --min=3 \
    --max=10 \
    --cpu-percent=80
```

### Update Operations
```bash
# Update container image
kubectl set image deployment/nginx-deployment \
    nginx=nginx:1.21

# Check rollout history
kubectl rollout history deployment/nginx-deployment

# Rollback to previous version
kubectl rollout undo deployment/nginx-deployment
```

## Monitoring and Debugging

### Deployment Status
```bash
# Get detailed deployment information
kubectl describe deployment nginx-deployment

# Check pod logs
kubectl logs -l app=nginx

# Get events related to deployment
kubectl get events --sort-by=.metadata.creationTimestamp
```

### Resource Utilization
```bash
# Check resource usage
kubectl top pods -l app=nginx

# Get detailed pod information
kubectl get pods -o wide
```

## Cleanup Operations

### Removing Resources
```bash
# Delete deployment
kubectl delete deployment nginx-deployment

# Verify removal
kubectl get all | grep nginx

# Clean up related resources
kubectl delete service nginx-deployment
kubectl delete hpa nginx-deployment
```

## Learning Notes

1. Always verify deployment status after creation
2. Use labels consistently for easier management
3. Monitor resource utilization during scaling
4. Maintain rollout history for quick rollbacks
5. Clean up unused resources to prevent cluster clutter

---

> 💡 **Best Practice**: Use declarative approaches for production environments to maintain version control and repeatability.

> ⚠️ **Warning**: Always backup configurations before major updates or scaling operations.

> 📝 **Note**: Some commands may require cluster-admin privileges. Ensure proper RBAC permissions are in place.