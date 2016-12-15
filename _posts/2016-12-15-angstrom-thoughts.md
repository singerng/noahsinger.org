---
title: First Thoughts on &aring;ngstromCTF
date: 2016-12-15 02:10:14 -0500
layout: blog
---

One of the main things I'll be talking about on this site is this competition I'm running called [&aring;ngstromCTF](http://angstromctf.com). &aring;ngstromCTF is an online high-school cybersecurity competition with all sorts of problems, ranging from cryptography to binary exploitation to forensics and web hacking. So far this year I've worked to revamp our competition platform to be scalable and maintainable.

Here's a partial list of the software I've put together so far:

* [Angular 2](https://angular.io/) as the main frontend application framework
    * [Angular CLI](https://github.com/angular/angular-cli) to manage Angular builds with [Webpack](https://webpack.github.io/)
* [Bootstrap 4](https://v4-alpha.getbootstrap.com/) as the CSS GUI library
    * [ng-bootstrap](https://ng-bootstrap.github.io/) for pure Angular implementations of Bootstrap components
    * [FontAwesome](http://fontawesome.io/) for awesome icons
* [TypeScript](https://www.typescriptlang.org/) for modern, reliable web scripting
* [Sass](http://sass-lang.com/) for modern, flexible stylesheets
* [DigitalOcean](https://www.digitalocean.com/) to scalably host the backend
* [Amazon AWS](https://aws.amazon.com/) to scalably host the frontend
    * Amazon S3 for static hosting of the frontend
    * Amazon Route 53 for DNS routing
* [Django](http://www.django-rest-framework.org/) as the root backend framework
* [Django REST framework](http://www.django-rest-framework.org/) to construct a RESTful API using Django
* [Swagger](http://swagger.io/) to expose the RESTful API in a standard format
    * [django-rest-swagger](http://marcgibbons.github.io/django-rest-swagger/) to expose the Django REST API in Swagger
    * [swagger-codegen](https://github.com/swagger-api/swagger-codegen) to generate TypeScript Angular 2 stubs for the API
* [PostgreSQL](https://www.postgresql.org/) as the backend database
* [Redis](https://redis.io/) as the backend cache manager
* [Ansible](https://www.ansible.com/) to automate server network deployment

I seem to be combining these tools in a relatively unique way, so I plan to write a lot about how I get everything to fit together. I hope it's interesting!
