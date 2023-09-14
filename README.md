# Classroom Jupyter

This is a very simplified Jupyter OnDemand app that the
Ohio SuperComputer center uses for classrooms.

It has fewer options and relies on classrooms being set in the
`cluster.d/cluster.yml`. 

## Example cluster configuration

The format for such a few classes.  The name of the key is the classroom name
and any keys within the struct are metadata for the classroom like which project
to use or how long the sessions can run for.

```yaml
# cluster.d/cluster.yml

v2:
  custom:
    classrooms:
      juypter:
        OSU_MATH_123:
          project: OSU1
        OSU_BIOLOGY_234:
          project: OSU2
        OU_CHEMISTRY_234:
          size: xlarge
          hours: 6
          project: OU1
```
