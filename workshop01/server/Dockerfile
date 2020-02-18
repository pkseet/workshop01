# What is the base image we are using
FROM node:latest

# define some environment variables
ENV APP_PORT=3000
ENV APP_ROOT=/app 
ENV MESSAGE="This is the day"
ENV DB_HOST=mydbserver
ENV DB_PORT=3306
ENV DB_PASSWORD=changeit
ENV DB_USER=root

# create the $APP_ROOT directory
# then go inside the directory
WORKDIR ${APP_ROOT}

# copy my files from notebook into ${APP_DIR}
# for folders have to specify target name
ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD public public
ADD views views
ADD config config

# install dependencies
# this will use package.json
RUN npm install


# configure healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1
    
# what port is application using
EXPOSE ${APP_PORT}/TCP

# how to run the program
ENTRYPOINT [ "node", "main.js" ]

# command line options
CMD [ "3000" ]
