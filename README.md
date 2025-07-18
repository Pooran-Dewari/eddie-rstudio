### eddie-rstudio

#### login to Eddie and launch rstudio
- make sure you login with ssh -Y option for X11 forwarding

```
qlogin -pe interactivemem 4 -l h_vmem=32G
source /exports/applications/support/set_qlogin_environment.sh
# check if X11 forwarding works fine, a clock should pop out with the command below
xclock
module load R
module load rstudio
rstudio
```

 - for some reason, rstudio on Eddie uses curl from anaconda, which doesn't work.
 - change path to circumvent this

```
# check which curl version is being used
> system("which curl")  
/exports/applications/apps/SL7/anaconda/5.3.1/bin/curl

# change path  
> Sys.setenv(PATH = paste("/usr/bin:/bin", Sys.getenv("PATH"), sep = ":"))

# check path  
> system("which curl")
/usr/bin/curl

# try installing
> install.packages("remotes")
Error: package 'remotes' is not available

# probably repos not set correctly
> getOption("repos")
CRAN "https://packagemanager.posit.co/cran/__linux__/rhel9/latest" 

# change repos
> options(repos = c(CRAN = "https://cloud.r-project.org"))

# should work now
> install.packages("remotes")
```
### Now we can install Seurat 5
```
remotes::install_github("satijalab/seurat", "seurat5")
```
