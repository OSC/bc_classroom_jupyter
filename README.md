# Classroom Jupyter App

This is a simplified Jupyter OnDemand app that the
Ohio Supercomputer Center uses for classrooms. This guide assumes you already know how to deploy Jupyter via Open OnDemand. 
It focuses on customizing the classroom app to support isolated and shared Python environments using OSC project spaces, where instructors
can share packages and materials with students.

OSC’s classroom Jupyter app allows instructors to:
- Launch isolated Python environments per course
- Share notebooks, datasets, and packages with students
- Customize session parameters per classroom

## Classroom Setup
Each classroom is assigned a dedicated project space on the cluster’s shared filesystem.
Within this space, instructors organize:

- ``materials``: Shared notebooks, datasets, and requirements
- ``venv``: Python virtual environment (created by instructor)
- ``data``: Optional large datasets
 
This structure ensures:

- Instructors have full write access
- Students have read-only access to ``materials/`` and ``venv/``
- Students copy materials into their own workspace at session start

## Environment Setup
``The Classroom_setup.erb`` script creates class directories in the project space along with the Jupyter environment. It also creates a classroom workspace for each student under their ``$HOME``.

 
## Sharing Materials
Shared materials are copied into the student’s workspace using rsync, as defined in ``before.sh.erb``.

 ## Cluster Configuration
The app relies on structured configuration in the ``clusters.d`` YAML files

To enable classroom-specific options, define class specific variables in the cluster configuration file:

```yaml
# /etc/ood/config/clusters.d/mycluster.yml
v2:
  custom_config:
    classrooms:
      jupyter:
        MATH101:
          project: PZS1234
          size: medium
          hours: 2
        BIO202:
          project: PZS5678
          size: large
          hours: 3
```


## Launch Workflow

- Instructor logs into ``class.osc.edu``
- Selects the Classroom Jupyter app
- Chooses their course from the dropdown
- Launches the session, installs required packages, and adds materials
 
The app:

- Activates the shared Python environment
- Copies materials to the user's workspace under ``$HOME/``
- Launches JupyterLab in the student’s workspace


