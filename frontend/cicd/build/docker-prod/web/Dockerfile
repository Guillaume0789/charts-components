FROM nginx:1.17-alpine

# Copy src
COPY --chown=nginx:nginx jenkins_release/charts-components /home/www
RUN sed -i 's/index.html//' /home/www/precache-manifest.*;
COPY --chown=root:root cicd/build/docker-prod/web/nginx.conf /etc/nginx/conf.d/default.conf
