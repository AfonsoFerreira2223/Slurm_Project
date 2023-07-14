## Test the config with



    sinfo

This should display node1 on the controller


    nano slurmtest.sh

```
     #!/bin/sh
    	    #Submit to a specifc node with a command e.g.
    	    # sbatch --nodelist=cn01 slurmtest.sh 
    	    #Submit to a random node with a command e.g.
    	    #sbatch slurmtest.sh
    	    #SBATCH --job-name=slurmtest
    	    node1 uptime
```

Execute with:

sbatch slurmtest && squeue
