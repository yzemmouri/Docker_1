FROM openjdk:8
WORKDIR /src/java
COPY . ./
RUN ["javac","Hello.java"]
ENTRYPOINT ["java","Hello"]