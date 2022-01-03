# Kubewrap

kubewrap is an kubernetes cli wrapper with a focus to explore the kubernetes REST API's leveraging the go libraries available along with golang and cobra package.

# Install  the cobra library:
```
 go get -u github.com/spf13/cobra/cobra
 ```
# Next, create the CLI skeleton 

```
cobra init --package-name kubewrap
```

It will initialize the “kubewrap” project with cobra the library. 


# Set up minikube

 Execute below commands inside kubewrap folder. Minikube must be installed as it'll need to check for default server to connect to.
```
 go install
 
 kubewrap

In powershell as admin:
New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing


Next add your binary to the path:

$oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
if ($oldPath.Split(';') -inotcontains 'C:\minikube'){ `
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
}
```

# Docker

```
docker build -o Kubewrap main.go 
```

```
docker pull Kubewrap:latest
```
```
docker run Kubewrap
```

# Install package dependencies
```
go get https://github.com/DanielPickens/Kubewrap.git
```

kubewrap is a root command and dig is a sub command to that
In the future, you could have a set of subcommands such as below
```
 kubewrap dig1
 ```
will list out all the pods
```
 kubewrap dig2
 ```
This will list out all the deployments…vice versa.
So, to extend the existing skeleton to have subcommand, just execute the cmd

Locate to the "kubewrap” folder. Again ignore here testkube
Now your flow would be → main.go -> root.go → dig.go
Now you could also see the dig.go file created in your existing file structure.


# Connect to cluster and config root.go

a. Connect to your cluster using “kubeconfig” REST API call → root.go
The changes required in “step a” needs to be implemented in the root.go wherein you just need to provide the path of your own config file.

Locate to the config in root.go and change the config file path above when required.
In root.go you just need to have above function which takes care of connecting to the minkube cluster using a REST call.  
b. Once connected, you would simply make a call to rest API to
```
“list pods available” → dig.go
```
Lastly, go to dig.go and follow the changes required to make a call to the REST API to list all the pods available in the cluster.
