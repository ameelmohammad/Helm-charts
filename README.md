# Helm-charts
![image](https://github.com/ameelmohammad/Helm-charts/assets/77770908/10b0d3d5-9b6b-4be7-b1a7-91a3f67770ad)
Helm:

Kubernetes has become the de facto standard for container orchestration and deployment. With the increasing complexity of Kubernetes applications, managing them manually can become a daunting task. This is where Helm, a package manager for Kubernetes, comes in.

Helm helps you manage Kubernetes applications by providing a way to define, install, and upgrade complex Kubernetes applications.

At its core, Helm uses charts, which are packages of pre-configured Kubernetes resources. These charts are used to define, install, and manage complex Kubernetes applications.

Helm charts can be used to define anything from a simple web application to a complex distributed system.

A Helm chart consists of a few files that define the Kubernetes resources that will be created when the chart is installed. These files include the Chart.yaml file, which contains metadata about the chart, such as its name and version, and the values.yaml file, which contains the configuration values for the chart. The templates directory contains the Kubernetes resource templates that will be used to create the actual resources in the cluster.

Using Helm charts, you can quickly and easily deploy complex Kubernetes applications. Helm charts also make it easy to manage application upgrades and rollbacks. With Helm, you can upgrade an application to a new version by simply updating the chart and running a Helm upgrade command. If something goes wrong, you can easily rollback to the previous version of the application using the Helm rollback command.

Helm charts are also highly customizable. You can define your own configuration values in the values.yaml file, and you can override these values at installation time using the Helm install command. This makes it easy to deploy the same application with different configurations in different environments, such as development, staging, and production.

One of the greatest benefits of using Helm is the large number of pre-built charts available in the Helm chart repository. The Helm chart repository is a centralized repository of pre-built charts that you can use to quickly deploy popular applications, such as WordPress, MySQL, and Prometheus. Using these pre-built charts can save you time and effort by allowing you to quickly deploy popular applications without having to build and configure them from scratch.

Helm charts are an essential tool for managing complex Kubernetes applications. With Helm, you can easily define, install, and manage complex Kubernetes applications, making it easier to manage your applications at scale. The Helm chart repository also provides a large number of pre-built charts, which can save you time and effort when deploying popular applications. If you’re not already using Helm, it’s definitely worth giving it a try.
here’s an example of a basic Helm chart for a simple web application:

First, create a new directory for your Helm chart:
mkdir my-web-app-chart
cd my-web-app-chart
2. Create a new file called Chart.yaml with the following contents:

apiVersion: v2
name: my-web-app
description: A Helm chart for a simple web application
version: 1.0.0
This file defines some basic metadata about your chart, such as its name, description, and version.

3. Create a new file called values.yaml with the following contents:

replicaCount: 3
image:
  repository: my-web-app
  tag: latest
  pullPolicy: IfNotPresent
service:
  name: my-web-app
  type: ClusterIP
  port: 80
ingress:
  enabled: false
This file defines the configuration values for your chart. In this case, it sets the number of replicas, the Docker image to use, and the service and ingress settings.

4. Create a new directory called templates, and create a file called deployment.yaml inside it with the following contents:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Chart.Name }}
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      app: {{ .Chart.Name }}
  template:
    metadata:
      labels:
        app: {{ .Chart.Name }}
    spec:
      containers:
        - name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
          imagePullPolicy: {{ .Values.image.pullPolicy }}
          ports:
            - name: http
              containerPort: 80
This file defines the Kubernetes deployment for your web application. It uses the configuration values defined in the values.yaml file to set the number of replicas and the Docker image to use.

5. Create another file called service.yaml inside the templates directory with the following contents:

apiVersion: v1
kind: Service
metadata:
  name: {{ .Values.service.name }}
spec:
  type: {{ .Values.service.type }}
  ports:
    - port: {{ .Values.service.port }}
      targetPort: http
  selector:
    app: {{ .Chart.Name }}
This file defines the Kubernetes service for your web application. It uses the configuration values defined in the values.yaml file to set the service type and port.

6. Finally, package your chart by running the following command:

helm package .
This will create a my-web-app-1.0.0.tgz file, which you can use to install your chart on a Kubernetes cluster using the Helm install command.

This is just a simple example, but Helm charts can be much more complex and can include multiple Kubernetes resources, such as services, deployments, statefulsets, and more. The templates can also include logic and control flow using the Go templating language, making it easy to generate dynamic configurations.
