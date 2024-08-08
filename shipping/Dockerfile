# Multi-stage Build

# Build Stage
FROM maven:3.8.6-openjdk-11 AS build

WORKDIR /opt/shipping

# Copy Maven project descriptor and resolve dependencies
COPY pom.xml /opt/shipping/
RUN mvn dependency:resolve

# Copy the source code and package the application
COPY src /opt/shipping/src/
RUN mvn package

# Run Stage
FROM openjdk:11-jdk-slim

EXPOSE 8080

WORKDIR /opt/shipping

# Copy the built JAR from the build stage
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

# Set environment variables
ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

# Run the application
CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]
