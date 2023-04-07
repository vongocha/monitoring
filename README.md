Monitoring a Linux host with Prometheus, Node Exporter, and Docker Compose
In this guide, you’ll learn how to run Prometheus and Node Exporter as Docker containers on a Linux machine, with the containers managed by Docker Compose. You’ll mount the relevant host directories into the Node Exporter and Prometheus containers, and configure Prometheus to scrape Node Exporter metrics and push them to Grafana Cloud. You’ll then install a preconfigured dashboard or create your own to visualize these system metrics.

Prerequisites
Before you begin you should have the following available:

A Grafana Cloud account. To create an account, please see Grafana Cloud and click on Start for free.
A Grafana Cloud API key with the Metrics Publisher role
A Linux machine
Docker and Docker Compose installed on your Linux machine
Step 1: Create the Compose file
In this step, you’ll create a docker-compose.yml file which will define our prometheus and node-exporter services, as well as our monitoring bridge network.

Open a file called docker-compose.yml in your favorite editor and paste in the following:

Step 3: Verify that metrics are being ingested
In this step, you’ll query your Prometheus metrics from Grafana Cloud.

Click Explore in the left-side menu to start. This will take you to the Explore view:

Explore view

At the top of the page, use the dropdown menu to select your Prometheus data source.

Use the Metrics browser to find the node_disk_io_now metric, then click on the job label and node label value. Recall that we set the job_name to node in our prometheus.yml configuration file.

Metrics dropdown

If you cannot see metrics in the dropdown, metrics are not being ingested. You can also confim ingestion by navigating to the billing dashboard.

If metrics do not appear after several minutes, check your work for typos, and make sure that both prometheus and node-exporter containers are running. Troubleshoot the logs with docker-compose logs -f .

Step 4: Configure a dashboard
In this step you’ll import a Grafana dashboard into your managed Grafana instance.

Official and community-built dashboards are listed on the Grafana website Dashboards page. Dashboards on this page will include information in the Overview tab about required configurations you may need to get the dashboard to work.

In this quickstart, we’ll use the Node Exporter Full dashboard. Note the dashboard’s ID: 1860.

In Grafana, click on Dashboards in the left-side menu to go to the Dashboards page.

Click New and select Import in the dropdown menu. Enter the dashboard’s ID and click Load. Select the appropriate Prometheus data source, and then click on Import.

Depending on your node exporter configuration, some panels may not function correctly. To learn how to configure node exporter to emit the required metrics, please see the node_exporter GitHub repo.

You can learn more about migrating and exporting dashboard in Export and import from the Grafana Cloud docs.

Conclusion
In this guide, you set up Prometheus and Node Exporter as Docker containers on a Linux machine to emit and scrape host metrics, with the containers managed by Docker Compose. You then imported a dashboard into your hosted Grafana instance to visualize and query these metrics.

From here, you can build additional panels and dashboards, and scrape metrics from other containers and systems. To learn more about building dashboards, please see Add a panel from the Grafana docs.
