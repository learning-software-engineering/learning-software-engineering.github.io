# Using SLURM for Machine Learning Tasks in HPC

## Table of Contents

1. [Introduction to SLURM?](#introduction-to-slurm)
2. [Advantages of Using SLURM in HPC](#advantages-of-using-slurm-in-hpc)
3. [Setting Up SLURM](#setting-up-slurm)
4. [Basic SLURM Commands](#basic-slurm-commands)
5. [Advanced SLURM Features](#advanced-slurm-features)
6. [Using SLURM for Machine Learning](#using-slurm-for-machine-learning)
7. [Best Practices and Tips](#best-practices-and-tips)
8. [Troubleshooting Common Issues](#troubleshooting-common-issues)
9. [Conclusion](#conclusion)
10. [Further Resources](#further-resources)

## Introduction to SLURM?

SLURM (Simple Linux Utility for Resource Management) is a highly efficient, robust, and scalable job scheduling system, used in High-Performance Computing (HPC) environments. SLURM is known for its scalability, supporting computing environments ranging from small clusters to systems comprising of thousands of nodes. This scalability is crucial in HPC, where computational demands can vary dramatically. With the recent surge in interest in machine learning and deep learning, SLURM has become a widely used tool for many researchers and developers. Its ability to efficiently schedule and manage diverse workloads, from data preprocessing and model training to inference, makes it ideal for the iterative and resource-intensive nature of machine learning tasks. In this guide, I will delve into how SLURM can be leveraged for machine learning tasks, offering practical advice, detailed command references, and best practices to help you effectively utilize SLURM in your ML projects.

## Advantages of Using SLURM in HPC

- **Efficiency in Resource Management**: Optimizes the use of available computational resources, reducing idle times and maximizing throughput.
- **Scalability and Flexibility**: Manages anything from a few nodes to clusters with thousands of nodes, catering to varying workload sizes.
- **Job Scheduling**: Prioritizes and queues jobs based on predefined policies, ensuring fair resource distribution and maximizing throughput.
- **User-Friendly Syntax**: Simplifies complex job management with intuitive commands and scripts.
- **Rich Feature Set**: Offers advanced scheduling, prioritization, and resource allocation capabilities.

## Setting Up SLURM

### Prerequisites

- Basic knowledge of Linux and HPC concepts.
- Access to a Linux-based HPC environment.

### Detailed Installation and Configuration

**Installation**: To install SLURM, follow the comprehensive steps in the [SLURM installation guide](https://slurm.schedmd.com/quickstart_admin.html). Here is a summary of that guide.

1. **Download SLURM**: Obtain the latest version of SLURM from the [official website](https://www.schedmd.com/downloads.php). Choose the version compatible with your Linux distribution.

2. **Dependencies**: Install necessary dependencies. Common ones include `munge` (for secure authentication), `openssl`, and various development libraries (`gcc`, `make`, `perl`, etc.).

3. **Compile and Install**: Unpack the downloaded source and compile SLURM using `./configure`, `make`, and `make install`. These commands will compile and install SLURM binaries, libraries, and default configurations.

**Configuration**: Create and configure `slurm.conf` according to your cluster's architecture. This includes setting up nodes, partitions, and resource limits.

1. **Create `slurm.conf`**: This is the primary configuration file for SLURM. You can start with a sample file provided in the source code (`etc/slurm.conf.example`) and modify it according to your cluster's specifications.

2. **Define Control Machine**: Specify your control node (the node that will manage the workload) in the `ControlMachine` parameter.

3. **Configure Nodes and Partitions**: Define your compute nodes under the `NodeName` parameter and group them into partitions (queues) using the `PartitionName` parameter.

4. **Setup Munge Authentication**: Ensure that the `munge` daemon is running on all nodes for secure communication.

5. **Control and Compute Daemons**: Understand the roles of `slurmctld` (control daemon) and `slurmd` (compute node daemon).

### Advanced Configuration (Optional)

1. **Accounting and Logging**: Set up SLURM's accounting feature for tracking and auditing jobs, and configure logging levels for troubleshooting.

2. **Resource Limits**: Configure limits on resources such as maximum job size, runtime, and number of jobs per user.

3. **Quality of Service (QoS)**: Define QoS levels to prioritize certain jobs or users. In the `slurm.conf` file you can define different QoS policies using the QoS parameter. Each policy can have settings like MaxWall, MaxTRES, Priority, etc., which dictate the maximum run time, resource limits, and priority levels.

## Basic SLURM Commands

- `sbatch`: Submits a batch job script to the scheduler.
- `srun`: Executes a command or job script in real-time.
- `scancel`: Cancels a scheduled or running job.
- `squeue`: Displays the queue of pending and running jobs.
- `sinfo`: Shows the status of SLURM nodes and partitions.

### Starting SLURM Services

1. **Start the Controller Daemon (`slurmctld`)**: On the control node, start the `slurmctld` daemon. Run `systemctl start slurmctld` and check the status by running `systemctl status slurmctld`.

2. **Start the Compute Node Daemons (`slurmd`)**: On each compute node, start the `slurmd` daemon. Run `systemctl start slurmd` and check the status by running `systemctl status slurmd`

3. **Verify the Setup**: Use `sinfo` and `scontrol show nodes` commands to check the status of the cluster and ensure that all nodes are communicating correctly with the controller.

### Testing Your Setup

1. **Run Test Jobs**: Submit simple test jobs using `sbatch` and `srun` to ensure that jobs are being scheduled and executed correctly on the compute nodes.

2. **Monitor Job Execution**: Use `squeue` and `sacct` to monitor these jobs and verify their completion status.

### Troubleshooting

- If nodes appear down or drained, check logs (typically under `/var/log/slurm/`) for errors.
- Ensure network connectivity and correct configuration of `munge` for authentication issues.
- For any issues with starting jobs, verify resource allocation and partition configurations.

Remember, each HPC environment is unique, and specific configuration details might differ. It's essential to collaborate with your system administrator and refer to SLURM's comprehensive documentation for environment-specific adjustments.

## Advanced SLURM Features

- **Job Arrays**: Handle large sets of similar jobs efficiently with job arrays.
- **GPU Scheduling**: Specific options for managing GPU resources for deep learning tasks.
- **Dependency Chains**: Create complex workflows with dependent jobs.
- **Quality of Service (QoS)**: Define priorities and resource limits for different job types.

## Using SLURM for Machine Learning

### Preparing Your Environment

#### 1. Software Modules

In HPC environments, managing software packages and libraries efficiently is crucial for machine learning tasks. The `module` command in SLURM is instrumental in this regard, allowing users to load and unload specific versions of software as needed. Here's how to utilize it effectively:

- **Understanding Module Environment**: Modules encapsulate software packages, enabling you to manage multiple versions without conflicts.

- **Loading Required Modules**: Before running ML scripts, load necessary modules. For example, use `module load python/3.8 tensorflow/2.4` to load Python and TensorFlow (adjust for available versions).

- **Listing Available Modules**: Use `module avail` to see all modules on the system, helping you find required software versions.

- **Custom Modules**: If your project requires custom modules, coordinate with system administrators to set these up.

- **Unloading Modules**: After completion or for switching versions, use `module unload` to maintain a clean environment.

- **Script Automation**: Include module load commands in your SLURM job scripts to ensure the correct environment setup when jobs run.

- **Persistent Module Changes**: For frequently used modules, consider adding them to your `.bashrc` or equivalent file for automatic loading in new sessions.

- **Resource Compatibility**: Ensure that your SLURM job script's resource requests align with the requirements of the modules you load.

Example SLURM job script for ML:

```bash
#!/bin/bash
#SBATCH --job-name=ml_task
#SBATCH --nodes=1
#SBATCH --time=01:00:00
#SBATCH --partition=standard
#SBATCH --gres=gpu:1

# Load necessary modules
module load python/3.8 tensorflow/2.4
module load cuda/11.0
```

# Execute the machine learning script

```python
python train_model.py
```

## Best Practices and Tips

### Resource Estimation

- **Understand the Task Requirements**: Different ML tasks have varying resource needs. Training is usually more resource-intensive than inference.
- **Benchmarking**: Run smaller versions of your task to gauge resource usage, providing a baseline for CPU, memory, and runtime requirements.
- **SLURM Tools**: Utilize `seff` on completed jobs to get a summary of resource usage, helping in future resource requests.
- **Incremental Adjustments**: Start with conservative estimates and adjust based on job performance and resource availability.

### Efficient Use of GPUs for Deep Learning

- **GPU Selection**: Choose the appropriate type of GPU for your specific task.
- **GPU Sharing**: Use SLURM's `--gres=gpu:1` to request GPUs and consider GPU sharing if feasible.
- **Optimizing GPU Workloads**: Ensure your ML/DL models fully utilize the GPU's capabilities through efficient batching and parallelization.

### Preemption and Checkpointing

- **Understanding Preemption**: Know your cluster's preemption policy to plan effectively.
- **Implementing Checkpointing**: Periodically save the state of your job to allow resumption if preempted.
- **Auto-Restart Feature**: Use SLURM's `--requeue` to automatically requeue your job if it's preempted.

## Troubleshooting Common Issues

### Job Failures

- **Analyzing Job Errors**: Check the job's error output and SLURM's job information for failure reasons.
- **Common Causes**: Include incorrect job scripts, insufficient resources, or software errors.
- **Resource Limit Exceeding**: If a job exceeds its allocated resources, it will be terminated. Adjust your job script accordingly.

### Resource Allocation Problems

- **Diagnose with `sinfo` and `squeue`**: Check the status of nodes and the job queue for issues.
- **Review Resource Requests**: Ensure your job's resource requests are within the cluster's limits.
- **Consult Cluster Policies**: Be aware of cluster-specific policies or limits set by administrators.

### Debugging and Log Analysis

- **SLURM Logs**: Check the SLURM logs (`/var/log/slurm/`) for cluster-wide issues.
- **Job-Specific Logs**: Review stdout and stderr logs of your job for application-specific messages.
- **Correlating Logs**: Compare timestamps between different logs for insights into complex issues.

## Conclusion

SLURM is an essential tool for efficiently managing machine learning workloads in HPC environments. With the right knowledge and best practices, it can significantly enhance the productivity and efficiency of computational research.

## Further Resources

- [SLURM Official Documentation](https://slurm.schedmd.com/documentation.html)
- [Interactive HPC and Machine Learning Tutorials](https://hpc-tutorials.llnl.gov/)
- [SLURM Community Forums](https://lists.schedmd.com/mailman/listinfo/slurm-users)
