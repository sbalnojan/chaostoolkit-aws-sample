# [WIP] Chaos Engineering in Action! Nuking AWS Things With Chaostoolkit to make your production system more robust

This is how a "weakness" looks like.

```
$ chaos run experiment.json
[2019-08-22 20:47:20 INFO] Validating the experiment's syntax
[2019-08-22 20:47:21 INFO] Experiment looks valid
[2019-08-22 20:47:21 INFO] Running experiment: Check if instance is there.
[2019-08-22 20:47:21 INFO] Steady state hypothesis: Instance is there
[2019-08-22 20:47:21 INFO] Probe: instance-is-there
[2019-08-22 20:47:21 INFO] Steady state hypothesis is met!
[2019-08-22 20:47:21 INFO] Action: stop-instance
[2019-08-22 20:47:21 INFO] Pausing after activity for 10s...
[2019-08-22 20:47:31 INFO] Steady state hypothesis: Instance is there
[2019-08-22 20:47:31 INFO] Probe: instance-is-there
[2019-08-22 20:47:32 CRITICAL] Steady state probe 'instance-is-there' is not in the given tolerance so failing this experiment
[2019-08-22 20:47:32 INFO] Let's rollback...
[2019-08-22 20:47:32 INFO] No declared rollbacks, let's move on.
[2019-08-22 20:47:32 INFO] Experiment ended with status: deviated
[2019-08-22 20:47:32 INFO] The steady-state has deviated, a weakness may have been discovered
```

What you already have in here is:

```
.
├── Pipfile                 # Dependencies. Run pipenv install
├── Pipfile.lock
├── README.md
├── example_minimal         # Read this, do it, understand the chaostoolkit setup.
│   ├── Makefile
│   ├── experiment.json
└── example_minmal_aws      # read this, run it, to understand the aws chaostoolkit setup.
    ├── Makefile
    ├── experiment.json
```

What's still missing:

- some terraform to set up an asg + ec2
- the chaostoolkit for that
- some terraform to set up an ecs fargate and
- the chaostoolkit for that.
- a proper list of probes and actions you can run (go through the code to find them...).

## The chaostoolkit (-aws)

The chaostoolkit is located at: https://chaostoolkit.org/
the extension this is created with is here: https://github.com/chaostoolkit-incubator/chaostoolkit-aws

The aws-kit has quite some actions & probes, for the following resource types.
The probes & actions are not well documented, here is a list of some,
for the rest you'll have to dig through the code.

- ASG
- Lambda
- CloudWatch
- EC2
- - [Actions](https://github.com/chaostoolkit-incubator/chaostoolkit-aws/blob/master/chaosaws/ec2/actions.py)
- - - stop_instance
- - - detach_random_volume
- - - terminate_instances
- - - ...
- - [Probes](https://github.com/chaostoolkit-incubator/chaostoolkit-aws/blob/master/chaosaws/ec2/probes.py)
- - - count_instances
- - - instance_staste
- - - ...
- ECS
- EKS
- ElastiCache
- ELBV2
- IAM
- RDS
