# Project Bolierplate
Frontend / Backend with Docker

# Sample Setup
## Angular & Symfony
- Requires NodeJs installed
- Requires Composer installed
- Optional: Symfony Installer

### Install Angular
- `cd apps`
- `npm install -g @angular/cli`
- `ng new frontend` (any other name requires changes in the Dockerfile)

### Install Symfony
- `cd apps`
- (if applicable) `symfony new backend` (any other name requires changes in the Dockerfile)
- (if applicable) `composer create-project symfony/skeleton backend` (any other name requires changes in the Dockerfile)

### Run all for development
- `docker-compose -f docker-compose.dev.yml up -d`
- `cd apps/frontend && ng serve` 

- Frontend URL: http://localhost:4200
- Backend URL: http://localhost:8002
