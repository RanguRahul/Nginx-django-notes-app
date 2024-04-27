# Simple Notes App
This is a simple notes app built with React and Django.

## Requirements
1. Python 3.9
2. Node.js
3. React

# Deploying a web-application using Nginx server and Reverse Proxy. 

What is Nginx?

Nginx is a popular open-source web server software which serves its clients web pages. Suppose you want to access some website (www.google.com), when you put this web address in the browser you will see the homepage(web-page) of google. Web server serves the web files i.e. the HTML, CSS, Javascript files to the client i.e. user.

In short it is a web server which serves the web pages to its clients as per the need and requirement.

Nginx is compatible with multiple operating systems, including Linux, Windows, and macOS, and it is commonly used alongside other web technologies such as PHP, Python, and Ruby on Rails.

Why Nginx ?

1. High performance: Nginx is known for its high performance and low resource usage. It is designed to handle a large number of concurrent connections and requests, making it a great choice for high-traffic 
   websites and web applications.

2. Scalability: Nginx can be easily scaled horizontally by adding more servers to handle increased traffic. It also supports load balancing, which distributes traffic evenly across multiple servers.

3. Flexibility: Nginx has a modular architecture, which means that it can be easily extended and customized with various modules to suit different needs.

4. Security: Nginx has built-in security features such as SSL/TLS encryption and support for secure communication protocols. It also has the ability to block malicious traffic and prevent common attacks such as 
   DDoS attacks.

5. Ease of use: Nginx is relatively easy to set up and configure compared to other web server software.

Architecture of Nginx

## Nginx

Install Nginx reverse proxy to make this application available

`sudo apt-get update`
`sudo apt install nginx`

![2](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/35a2a5c0-a997-4ed5-9264-91bc441f6502)

![3](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/030c5bc4-1d2a-41fc-8f6e-6ad02b950036)

Check if the Nginx is in running state. Use command:

![4](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/b07f7421-592c-4f83-a5fe-d73748e90ff6)

Also you can take the public IP of the server and try accessing it in browser,to check if the Nginx is installed properly.


![5](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/28eed7b2-0901-4a6e-b712-980c7a7d15e3)

This page is been accessed from /var/www/html, git clone https://github.com/RanguRahul/Nginx-django-notes-app.git


You can check the Nginx configuration files here:

![6](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/f4b183ea-a260-407b-ba3f-7915ce32c772)

Now install docker

![7](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/b9e47de8-f45e-40d9-a05e-a47408e8ae3e)

Check docker status:

![8](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/d965b16f-645a-4e09-87fb-cbe44a29dfc0)

Now check if docker is working fine.



![9](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/0ac3bdf1-338d-4915-8645-4cd210889204)

Here is the Dockerfile :


![10](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/97c1fd65-5c39-4658-aa05-9968e7f4da83)


Now we will start the build process of the application. Use command :

![12](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/f696b962-a885-40fc-a65f-0b0c69bb6e33)


![11](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/3657893e-8988-4c57-879c-1caa2ade5f0a)

Now using this image we will create a container . Use below command:



![13](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/ac976174-b47c-495c-8102-d77fb16e487d)

Now do #docker ps and check if the container is created properly and it has been tagged to the 8000 port so that we can access the same on that port.



![14](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/5aa9f474-7aa7-4b73-a4d3-47da7fce2dc4)

#curl -L <local_url>:<External-Ip> curl -L http://172.0.0.10:8000

This application is now running on the local host and we can check it using the command:

![15](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/c049ba1c-2d7f-47fe-9af0-cc7e5a369039)

But we want to give access to the application by using the concept of reverse proxy so that the clients can access the same.

For this we need to change the configuration of Nginx so for that go to

#/etc/nginx/sites-enabled


![17](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/f8f8f318-0bb2-416b-8958-86db91703521)

Now we will update the default file for changing the configuration.

![16](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/8c47a0cc-980b-42d6-b173-ebe50e979e8c)

Now you can access the application using the IP address.

![22](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/26474acf-0c84-4e78-ba23-851c85697e41)


Now the app is accessible but we are not able to update or delete the notes here because the backend code is not updated here to store such data.

For this we need to copy all the static files of the application to the location Nginx root folder /var/www/html so that we can access it.


![18](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/e1ad0b28-64d2-4c2b-9cdd-bb48b5ddee06)

Now we need to update the location /api for the backend page of the server.

Go to /etc/nginx/sites-enabled location and update the code.

![19](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/fdb63d6d-f916-4600-b9a8-50bff3a16250)

Here we have added a proxy address for the incoming traffic.

service nginx restart

After adding this you need to restart the nginx so that the updates will work. Use below command to restart nginx.


![20](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/6bec69e9-07bd-4a23-82eb-c866b48f3814)

Now you can access the application using the IP address.

![21](https://github.com/RanguRahul/Nginx-django-notes-app/assets/120587828/c62911e6-1815-41b9-ab98-0a34834ae377)



