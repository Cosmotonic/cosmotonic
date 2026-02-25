# costmotonic

Enter Server: ssh root@167.71.54.218

vagrant status

# use reserved IP 
ssh-keygen -R 159.89.215.163 
ssh -i ~/.ssh/id_ed25519 root@159.89.215.163

# UPDATE WEBSITE MED LATEST Rerun docker to update website with new code 
git pull
docker build -t mysite .
docker stop cosmotonic && docker rm cosmotonic && docker run -d -p 80:80 --name cosmotonic mysite

# Vagrant commands 
