# Solution
  - Use docker run -d infracloudio/csvserver:latest 
  - Check error using docker logs `container_id`
    ```console
    2021/01/20 14:29:19 error while reading the file "./inputdata": open ./inputdata: no such file or directory
    ```
  - Create a `gencsv.sh` file.
    ```console
    vi gencsv.sh
	```
> **NOTE**: gencsv.sh file is provided in solution directory
 
  - Run the script `gencsv.sh`
    ```console
    chmod +x gencsv.sh
    ./gencsv.sh
	```
  - It will create a file name called as `inputFile` which we need to provide in container at path `/csvserver`
  - Run the docker in detached mode:
    ```console
    docker run -d -v /root/inputFile:/csvserver/inputdata infracloudio/csvserver:latest
    ```
  - Remove running container using command `docker rm -f container_id`
  - Use `docker inspect` to check the port exposed in container
    ```console
    docker inspect container_id
	  ```
  - To set environment variable use `-e` and `-p` is use to forward port.
    ```console
    docker run -d -p 9393:9300 -v /root/inputFile:/csvserver/inputdata -e CSVSERVER_BORDER=Orange infracloudio/csvserver:latest
    ```
## Part II
  - `docker-compose.yml` file is available at **solution** directory.
  - Use `docker-compose up` command to run container. 
    ```console
    docker-compose up
    ```

## Part III
- Prometheus requires prometheus configuration file called as `prometheus.yml` which is provided in solution directory.
- Change ip address and port in `prometheus.yml` file.
  ```console
  static_configs:
      - targets: ['192.168.0.18:9393']
  ```
- Use `docker-compose up` command to run containers.
