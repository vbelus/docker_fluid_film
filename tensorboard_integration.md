# To view tensorboard from a browser on your local machine, with trainings on a docker on a remote server

- Get the docker and vm IPs with `hostname -i`
- Chose a port for your server, for example 6012
- in the docker, run `tensorboard --logdir tensorboard_logs/ --host $DOCKER_IP --port $SERVER_PORT`\
If you want it to run in the background, `nohup tensorboard --logdir tensorboard_logs/ --host $DOCKER_IP --port $SERVER_PORT &`
- On your local machine, run `ssh your_vm_username@$VM_IP -L 6006:$DOCKER_IP:$SERVER_PORT`
- You can then go to `https://localhost:6006` in your local browser
