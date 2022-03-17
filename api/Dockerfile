# Pull base image
FROM python:3.9
#Folder where to place files in container
WORKDIR /app
#port to expose, check in code
EXPOSE 5050
# copy pipfile and pipfile lock to app dir
COPY Pipfile Pipfile.lock ./
#packages to install based on pipfile
# even though virtual env is not reqd in container
# we create it to have all dependencies in txt file
# and then install those using pip
RUN pip install pipenv
RUN pipenv lock --requirements > requirements.txt
# pip to install dependencies
RUN pip install -r requirements.txt
# copy remaining files , not copied with dependency because each step builds a layer
# each layer is cached
# if we don't change dependencies we dont have to rebuild that step
COPY . ./
# to run the app, cont will start with this process
CMD ["python","main.py"]

