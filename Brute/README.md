# arpg-brute.cs.colorado.edu aka Brute

Brute is our lab GPU powerhouse machine. To reserve time on this machine, use the [google calendar](https://calendar.google.com/calendar/u/1?cid=Y29sb3JhZG8uZWR1X29jbWl0Njhjc21lMDg5dnQ4bW1odTIwN2dzQGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20).  

No-one has set up a remote desktop client yet, so right now, you can either ssh or visit the lab in person. You need to be in the university VPN to ssh into Brute. Instructions for the VPN are [here](https://oit.colorado.edu/services/network-internet-services/vpn). If you want to install a remote desktop, please do, and add the details to this document. If you want a way to view images and figures without installing a remote desktop, see the [Tips and Tricks](#tips-and-tricks) section.

## Hardware

### Storage 

Brute currently has 500GB SSD for the partition hosting `/home/` which includes all user home directories. As a result, the SSD frequently runs out of space. Therefore, we request that all data and models are stored on the two storage hardrives, `/media/bigdrive/`(2TB) and `/media/giantdrive/`(8TB). All data should also be backed up to another machine or cloud location, as data losses have occurred when users were purged after graduation. 

#### Space Troubleshooting

Is the disk full again? Here are some commands to locate large directories and files.

- Find out which disks are full `df -h`
- Interactive file structure browsing of user directories `ncdu \home\`
- Comprehensive search for large files including docker, excluding media drives `sudo du -h / | grep -v /media | grep ^[0-9]*G`

Frequent offenders are docker images and conda packages

- Purge unused and dangling docker images `docker system prune`
- Purge unused conda packages `conda clean -a`

### GPUs

Brute has 2 P6000 GPUs. When reserving use, specify which GPU you are reserving, i.e. 0 or 1.   

## Software

### CUDA

Brute currently has 3 CUDA versions installed, 10.2, 9.0, 8.0. The newest version is symlinked to /usr/local/cuda/. 

If you want to use one of the older versions, please set user variables to reflect the desired version. Do not change the symlink, as other users may be relying on it. 

If you want to update to a newer CUDA version, please start a discussion on teams to determine whether updating the symlink is appropriate. 

### conda

Conda is a python environment manager that is strongly recommended for installing python packages on Brute.

We are currently using a multi-user conda installation located at at `/opt/miniconda3/`. This should allow us to share packages and save some redundant installations. If you have not previously installed anaconda locally, all your new environments should automatically use this installation.

Otherwise to move your pre-existing conda environments to this new location follow these steps :

1. Check `which conda`  It should now point to `/opt/miniconda3/bin/conda`, but it might not depending on your `~/.bashrc` configuration.
	
2. To check what environments you have on your local conda installation, use `<conda_root>/bin/conda env list`
	
3. Activate the environment using its location, not it's environment name, as it is now not in the default environment location for the new installation. For example, `conda activate /home/cecilia/anaconda3/envs/deeplab`
	
4. Write a spec list for the environment `conda list --explicit > spec-list.txt` WARNING: The spec list will not include packages installed with pip.
	
5. Recreate the environment in the new shared directory `conda create --name env_name --file spec-list.txt`
		
6. Remove your old conda installation in your home directory including entries in the `~/.bashrc` file

I recommend to use an environment name that includes your user name, i.e. `python3_cecilia`, so that we can remove your environments once you graduate. It will also help you find your environments 

## Accounts

Contact Cesar Galen for a Brute account. @Cesar if you want to add notes about setting up new accounts here, please do.

## Tips and Tricks

### Use tmux or screen to run code when you log out

If you haven't used remote connections extensively before, you might be unpleasantly surprised when your code stops running because your VPN expires or you lose network connectivity. To avoid this, use `tmux` or `screen`. These are "terminal multiplexers" which make virtual terminal consoles which will persist after you log out. Just google for a tutorial. They both have lots of functionality which would be too detailed to cover here.

### Using Jupyter Notebooks remotely for Graphics

You can port forward a jupyter notebook to view images and figures on Brute remotely. 

1. On Brute, start a jupyter notebook instance in a tmux session `jupyter notebook --no-browser --port=XXXX`

2. On your local machine, set up forwarding to port YYYY, `ssh -N -f -L localhost:YYYY:localhost:XXXX user@arpg-brute.cs.colorado.edu`

3. On your local machine, open a browser to `http://localhost:YYYY` 

4. Now you can either browse the directory structure and open images directly, or use a notebook to open images or generate figures with python or any other jupyter supported language. 



