# Smart Auto-Scaler for Cost Optimization

## Overview
This Kubernetes controller dynamically scales pods based on real-time **cloud cost metrics** and application usage instead of just CPU/memory thresholds. It helps optimize costs by analyzing cloud billing data and adjusting workloads accordingly.

## Features
- **Monitors Pod Costs**: Fetches cost data for each running pod.
- **Dynamic Scaling**: Suggests scaling down expensive workloads.
- **Cloud API Integration**: Placeholder for AWS Cost Explorer / GCP Billing API.
- **Configurable Thresholds**: Define cost limits for scaling actions.
- **Runs as a Kubernetes Controller**: Uses `client-go` to interact with cluster resources.

## Installation
### Prerequisites
- A running **Kubernetes cluster**
- `kubectl` configured for your cluster
- Go 1.18+

### Steps
1. Clone the repository:
   ```sh
   git clone https://github.com/ametow/autoscaler-cost-optimization.git
   cd autoscaler-cost-optimization
   ```
2. Build and push the Docker image:
   ```sh
   docker build -t [docker-username]/autoscaler-cost-optimization:latest .
   docker push [docker-username]/autoscaler-cost-optimization:latest
   ```
3. Deploy to Kubernetes:
   ```sh
   kubectl apply -f k8s/deployment.yaml
   ```

## Configuration
Modify the `config.yaml` file to set cost thresholds and scaling behavior:
```yaml
costThreshold: 10.0  # Maximum allowed cost per pod in USD
checkInterval: 60    # Check interval in seconds
```

## How It Works
1. The controller **fetches a list of all running pods**.
2. It **queries cloud cost APIs** to get the real-time cost of each pod.
3. If a pod exceeds the configured cost threshold, it **triggers a scale-down recommendation**.
4. Future enhancements will allow **auto-scaling actions** instead of just recommendations.

## Future Enhancements
- **AWS Cost Explorer / GCP Billing API Integration**.
- **Auto-scaling logic** to adjust deployment replicas dynamically.
- **Custom Resource Definition (CRD)** to configure thresholds per namespace.

## Contributing
Feel free to contribute by submitting a pull request or opening an issue!

## License
This project is licensed under the MIT License.

