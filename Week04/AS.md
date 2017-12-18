# AWS - Auto Scaling

## Auto Scaling Characteristics
- Is a web service designed to launch or terminate EC2 instances automatically based on user-defined policies, schedules, and health checks.
- Helps to ensure that you have the correct number of EC2 instances available to handle the load for your application
- You can specify scaling policies, then Auto Scaling can launch or terminate instances on demand as your application needs increase or decrease.
- You can specify the minimum number of instances in each Auto Scaling group, and Auto Scaling ensures that your group never goes below this size.
- Generally, Auto Scaling is orchestrated by Amazon CloudWatch

![autoscale](http://docs.aws.amazon.com/autoscaling/latest/userguide/images/as-basic-diagram.png)

## Auto Scaling Components

### Launch configuration
- A Launch configuration is a template that an Auto Scaling group uses to launch EC2 instances.
- Launch configuration defines how Auto Scaling should launch your EC2 instances.
- You could create a new launch configuration using the attributes from an existent EC2 instance.
- When you create a launch configuration, you specify information for the instances such as the ID of the AMI, the instance type, a key pair, security groups, and a block device mapping

### Auto Scaling Group
- Is a collection of EC2 instances, so they can be treated as a logical unit for the purposes of scaling and managment.
- You can only specify one launch configuration for an Auto Scaling group at a time.
- If you want to change the launch configuration for an Auto Scaling group, you must create a launch configuration and then update your Auto Scaling group with the new launch configuration.
- An Auto Scaling group can have more than one scaling policy attached to it any given time. 

### Scaling plans
- Tells Auto Scaling when and how to scale.
- You can base a scaling plan on the occurrence of specific conditions (dynamic scaling) or on a schedule.

#### Maintain current instance levels at all times
- You can configure your Auto Scaling group to maintain a minimum or specified number of running instances at all times.
- When Auto Scaling finds an unhealthy instance, it terminates that instance and launches a new one.
- For more info see the [AWS Documentation](http://docs.aws.amazon.com/autoscaling/latest/userguide/as-maintain-instance-levels.html)

#### Manual scaling
- Specify only the change in the maximum, minimum, or desired capacity of your Auto Scaling group
- Auto Scaling manages the process of creating or terminating instances to maintain the updated capacity
- For more info see the [AWS Documentation](http://docs.aws.amazon.com/autoscaling/latest/userguide/as-manual-scaling.html)

#### Scale based on a schedule
- You know exactly when you will need to increase or decrease the number of instances in your group, simply because that need arises on a predictable schedule.
- Scaling by schedule means that scaling actions are performed automatically as a function of time and date.
- For more info see the [AWS Documentation](http://docs.aws.amazon.com/autoscaling/latest/userguide/schedule_time.html)

#### Scale based on demand
- A more advanced way to scale your resources, scaling by policy, lets you define parameters that control the Auto Scaling process.
- For example, you can create a policy that calls for enlarging your fleet of EC2 instances whenever the average CPU utilization rate stays above ninety percent for fifteen minutes.
- You should have two policies, one for scaling in (terminating instances) and one for scaling out (launching instances), for each event to monitor.
- For more info see the [AWS Documentation](http://docs.aws.amazon.com/autoscaling/latest/userguide/as-scale-based-on-demand.html)


## Auto Scaling Lifecycle
The EC2 instances in an Auto Scaling group have a path, or lifecycle, that differs from that of other EC2 instances. The lifecycle starts when the Auto Scaling group launches an instance and puts it into service. The lifecycle ends when you terminate the instance, or the Auto Scaling group takes the instance out of service and terminates it.

*You are billed for instances as soon as they are launched, including the time that they are not yet in service.*

![lifecycle](http://docs.aws.amazon.com/autoscaling/latest/userguide/images/auto_scaling_lifecycle.png)

### Scale Out
- Manually increase the size of the group
- Create a scaling policy to automatically increase the size of the group based on a specified increase in demand
- Set up scaling by schedule to increase the size of the group at a specific time
- When a scale out event occurs, the Auto Scaling group launches the required number of EC2 instances, using its assigned launch configuration. These instances start in the _Pending state_.
- When each instance is fully configured and passes the Amazon EC2 health checks, it is attached to the Auto Scaling group and it enters the _InService state_.

### Instances in Service
### Scale In
### Attach an Instance
### Detach an Instance
### Lifecycle Hooks
### Enter and Exit Standby
