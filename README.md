# CSSE6400 Week 6 Practical

This practical extends the previous TaskOverflow ECS deployment by adding:

- an Application Load Balancer
- a target group with health checks
- ECS service load balancing
- ECS auto scaling based on CPU utilisation
- load testing with k6

## Files

- `main.tf` - provider and shared settings
- `db.tf` - PostgreSQL database
- `ecs.tf` - ECS cluster, task definition, and service
- `lb.tf` - load balancer, target group, listener, and DNS output
- `autoscaling.tf` - auto scaling target and policy
- `k6.js` - load test script

## Deploy

```bash
terraform init
terraform plan
terraform apply
````

## Test

```bash id="y3tsum"
curl "http://$(terraform output -raw taskoverflow_dns_name)/api/v1/health"
curl "http://$(terraform output -raw taskoverflow_dns_name)/api/v1/todos"
```

## Load Test

```bash id="7int7v"
BASE_URL="http://$(terraform output -raw taskoverflow_dns_name)" k6 run k6.js
```

## Result

The TaskOverflow service was successfully deployed behind an ALB, passed health checks, and scaled under load.

## Clean Up

```bash id="7qf2ql"
terraform destroy
```

## Note

The local `credentials` file must not be committed.

````id="f0hi8k"

如果你想直接覆盖 `README.md`，就跑这个：

```bash id="b3gimf"
cat > README.md <<'EOF'
# CSSE6400 Week 6 Practical

This practical extends the previous TaskOverflow ECS deployment by adding:

- an Application Load Balancer
- a target group with health checks
- ECS service load balancing
- ECS auto scaling based on CPU utilisation
- load testing with k6

## Files

- `main.tf` - provider and shared settings
- `db.tf` - PostgreSQL database
- `ecs.tf` - ECS cluster, task definition, and service
- `lb.tf` - load balancer, target group, listener, and DNS output
- `autoscaling.tf` - auto scaling target and policy
- `k6.js` - load test script

## Deploy

```bash
terraform init
terraform plan
terraform apply
````

## Test

```bash
curl "http://$(terraform output -raw taskoverflow_dns_name)/api/v1/health"
curl "http://$(terraform output -raw taskoverflow_dns_name)/api/v1/todos"
```

## Load Test

```bash
BASE_URL="http://$(terraform output -raw taskoverflow_dns_name)" k6 run k6.js
```

## Result

The TaskOverflow service was successfully deployed behind an ALB, passed health checks, and scaled under load.

## Clean Up

```bash
terraform destroy
```

## Note

The local `credentials` file must not be committed.
