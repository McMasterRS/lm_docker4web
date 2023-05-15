---
layout: default
title: Creating a Docker Image
parent: Part 2 - Docker Compose
nav_order: 2
---

## Creating a Docker Image

### What is a Docker Image?

A Docker image is a collection of self-contained files that act as a template for creating containers. Images can be seen as frozen or read-only containers that are exchanged through the Docker registry. When you download an image from the Docker registry and spin up a container from the downloaded image, you are essentially creating a writable layer on top of the existing read-only layers bundled with the image.  

### Running a Base Nginx Image

Nginx is an open-source web server, that is now also used a reverse proxy, HTTP cache, and a load balancer. Nginx was built with a focus on high performance and low memory usage.  

1. Create a base container using the official Nginx image:  
`docker create --name nginx_base -p 80:80 nginx:alpine`  
Note that the `create` command creates the container but does not actually start it. You can verify that the `nginx_base` is not running using the `docker container ls` command.  
2. Verify that the image was successfully created by listing all existing images using the `docker images -a` command.  
3. Start the `nginx_base` container:  
`docker start nginx_base`  
4. Visit [http://localhost](http://localhost) on your browser and you should be presented with the Nginx landing page.  
5. Modify the container to display a custom index page:  
    1. Create an `index.html` file on your machine using the editor of your choice.  
    2. Paste the following HTML code into the `index.html` file.  

    ```html
    <html>
    <head>
    <title>Hello World</title>
    </head>
    <body>
    <h1>Hello World!</h1>
    </body>
    ```

    3. Use the `docker cp` command to copy the file over to the running `nginx_base` container:  
    `docker cp index.html nginx_base:/usr/share/nginx/html/index.html`
    4. Reload your browser and you should presented with a new updated "Hello, World" page you just created!  
6. Create an image from your container using the following command:  
`docker commit nginx_base`  
Run the `docker images -a` command and verify that there is a new image that was created recently. The image will not have a repository or tag.  
7. Tag the image:  
`docker tag <Image ID> my_image`  
Make sure to replace `<Image ID>` with your own image's ID found by running the `docker images -a` command. In this example, `my_image` is the tag name that we chose for this image. Feel free to pick any tag name that conforms to the naming convention (i.e., a tag name must be valid ASCII and may contain lowercase and uppercase letters, digits, underscores, periods and hyphens. A tag name may not start with a period or a hyphen and may contain a maximum of 128 characters.).  
After tagging the image, run the `docker images -a` command again and verify that the image now has a tag.  
8. Run the `docker container ls` command and verify that the original container that you started in Step 3 is still running.  
9. Stop the original container:  
`docker stop nginx_base`  
10. You can now create and run containers from the image you created. As previously discussed, you can create and run containers from an image in one command:  
`docker run --name my_new_container -d -p 80:80 my_image`

In the next section, we will detail how to create a Docker image for a Next.js website serving from a Nginx server using Docker Compose.    
