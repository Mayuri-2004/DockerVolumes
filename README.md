# Docker Volumes

## What is a Docker Volume?
A **Docker Volume** is used to store data outside the container’s filesystem.  
It helps in **data persistence**, so data is not lost when a container stops or is deleted.

### Why use Docker Volumes?
- Data remains safe even if container is removed
- Managed by Docker
- Best for databases and application data
- Easy to reuse and migrate

---

## Types of Docker Volumes
1. **Bind Volume**
2. **Named Volume**
3. **Anonomous Volume** 

---

## Docker Volume Commands (Step by Step)
### 1.Bind Volume: 
    A bind volume connects a folder from your host system (your computer) directly to a folder inside the container.
        

1. Install Docker
2. create directory(myvolume) inside create file (index.html)
3. create a volume
    -  docker run -d --name mycont -p 80:80 --volume /home/ubuntu/myvolume:/usr/share/nginx/html nginx
4. Go inside this Container and check
    - docker exec -it mycont /bin/bash
5. Share data to another container 
   - Create a container (mycont2)
 docker run -d --name mycont1 -p 80:80 --volume /home/ubuntu/myvolume:/usr/share/nginx/html nginx
6. Go inside mycont2 and  and check data will share


![](/img/bind%20volume.png)

---

### 2.Named Volume: 
    A Named volume is managed completly by docker. You give if a name and docker stores it in its default location
    (/var/lib/docker/volume)

1. Create volume
   - docker volume create myvolume
   - Map volume to container    
   - docker run -d --name mycont -p 80:80 -v myvolume:/usr/share/ nginx/html nginx  
2. Go inside the container and create file
   - docker exec -it mycont /bin/bash
3. Create another container 
   - docker run -d --name mycont1 -p 80:80 -v myweb:/usr/share/   nginx/html nginx   
4. Go in /var/lib/docker, cd volumes, cd myweb, ls,cd _data, ls
5. Check data will be share

![](/img/Named%20Volume.png)

---

### 3.Anonomous Volume:
    A anonomus volume is created automatically by docker when you use -v but dont give it name

1. Create volume
     - docker volume create myvolume
     - Map volume to container
     - docker run -d --name mycont -p 80:80 -v myvolume:/usr/share/ nginx/html nginx  
2. Go inside the container 
     - docker exec -it mycont /bin/bash
     - create a index.html Page 
3. Create another container
     - docker run -d 8080:80 --name mycont2 --volumes-from mycont1 nginx
4. Go inside the mycont2 and check the data will be share             
     - docker exec -it mycont2 /bin/bash  

    ![](/img/anonomous%20volume.png) 

    ---

    ## Conclusion
    This project helped me understand how Docker Volumes are used to store data permanently outside containers. I learned how volumes keep data safe even when containers are removed or restarted, making applications more reliable and production-ready.

    ---