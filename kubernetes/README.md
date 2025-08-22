Why kubernetes?
---------------
The Problem Before Kubernetes
  - Apps used to run on bare metal servers → hard to scale, costly.
  - Then came virtual machines → better, but heavy.
  - Then came containers (Docker) → lightweight, portable, fast.

But running lots of containers in production is hard:
  - How to start/stop 100s of containers?
  - How to restart if one crashes?
  - How to scale up during peak traffic?
  - How to load balance traffic between containers?
  - How to update without downtime?


Kubernetes (aka K8s) is a container orchestration system.
It automates the deployment, scaling, and management of containers.

Think of it as the “operating system for your containerized apps.”
