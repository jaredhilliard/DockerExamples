FROM openjdk:8-jdk-alpine AS builder
# start with the entire jdk so that we can compile the .java files
WORKDIR /out
# Set the working directory, rather than letting it be created automatically.
COPY *.java .
# change this line as necessary for each individual java project.
RUN javac Hello.java

# no need to keep the entire jdk, we just need the runtime environment.
FROM openjdk:8-jre-alpine
# now we know exactly where to copy from.
COPY --from=builder /out/*.class .
CMD ["java", "Hello"]
