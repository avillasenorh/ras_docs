# How to run your own data


```
#!/usr/bin/env bash
set -u

[[ $# != 1 ]] && { echo "usage: run_ras.sh parfile"; exit 1; }
[[ ! -s $1 ]] && { echo "ERROR: parameter file does not exist: $1"; exit 1; }

cur_dir=${PWD}
parfile="$1"

ras_dir=${HOME}/repos/rapidalignerseismic
[[ ! -d $ras_dir ]] && { echo "ERROR: rapidalignerseismic directory does not exist": exit 1; }
[[ ! -s $ras_dir/singularity_bashrc ]] && { echo "ERROR: singularity_bashrc does not exist": exit 1; }

cp ~/.bashrc ~/.bashrc_save
cp $ras_dir/singularity_bashrc ~/.bashrc

cd $ras_dir

/bin/rm -f runAll.$$.sh

touch runAll.$$.sh
echo "source ~/.bashrc"                                                 >> runAll.$$.sh
echo "conda activate rapidSis"                                          >> runAll.$$.sh
echo "#pip install mpi4py"                                              >> runAll.$$.sh
echo '#python -c "import mpi4py" 2> /dev/null || pip install mpi4py'    >> runAll.$$.sh
echo "cd notebooks"                                                     >> runAll.$$.sh
echo "mpirun -n 1 python ras_multiGPU.py -m Standard -r $parfile"       >> runAll.$$.sh
echo "conda deactivate"                                                 >> runAll.$$.sh
echo "exit"                                                             >> runAll.$$.sh
chmod 755 runAll.$$.sh

/bin/cp $cur_dir/$parfile notebooks
singularity exec --nv --bind /scratch2 --bind /sismo1 Container_rapid.simg ./runAll.$$.sh

#sleep 20

/bin/rm -f ./runAll.$$.sh

cp ~/.bashrc_save ~/.bashrc
```

