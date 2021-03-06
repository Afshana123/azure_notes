# Cloud Academy 
# AZ-104 Exam Preparation: Microsoft Azure Administrator

## Introduction 
The AZ-104 exam tests your knowledge of five subject areas.

We’ll start with managing Azure identities and governance. The first part of this section is all about Azure Active Directory, which is a managed version of Microsoft’s tried and true directory software for managing users, groups, and other identities. 

Next, we’ll cover role-based access control. This is how you can give users the right level of access to resources so they don’t have more privileges than they need.

The final topic in this section is managing subscriptions and governance. Aside from learning the basics of working with subscriptions, you’ll also learn how to maintain governance by applying policies to subscriptions and resources. Azure enforces these policies to prevent actions your organization doesn’t want to allow.

Next, we’ll get into implementing and managing storage. This section is, of course, mostly about Azure Storage, including everything from shared access signatures to importing data with the AzCopy tool to configuring storage tiers. It also covers how to centralize file shares using Azure File Sync.

Then you’ll learn how to deploy and manage compute resources. Azure has quite a few different types of compute resources where you can deploy your applications. The traditional way is to use virtual machines. This gives you full control of your servers, but it requires you to maintain them.

Creating a new VM on Azure is pretty easy, but this section shows you how to deploy VMs at an enterprise level. You’ll learn how to set up high availability and autoscaling and also how to automate the deployment of VMs using Azure Resource Manager.

Another approach that’s becoming very popular is to build applications as a collection of microservices. This normally requires the use of containers, such as Docker. If you use containers, then you’ll also need a way to provision, schedule, and manage them. This is also known as container orchestration, and the most popular orchestrator right now is Kubernetes.

If you don’t want to worry about dealing with the underlying compute resources, then you can use Azure App Service. It lets you host web and mobile applications without having to manage the servers that run them. 

After that, we’ll go into configuring and managing virtual networks, which is the biggest section of the exam. Again, this is about setting up enterprise-grade networks. You’ll learn how to connect virtual networks together using VNet peering and network gateways, how to configure both private and public DNS zones for name resolution, and how to secure your VNets using Network Security Groups.

We’ll also cover advanced virtual networking. An important part of this section is showing different ways to distribute an application’s load across multiple VMs. One method is to use Azure Load Balancer and another is to use Azure Application Gateway. Azure Load Balancer works at layer 4 of the network stack, so it routes TCP and UDP packets. Azure Application Gateway works at layer 7, so it routes at the HTTP layer. This gives it the ability to do more than Azure Load Balancer. For example, it includes a web application firewall that protects your applications from common exploits, such as SQL injection and cross-site scripting attacks.

This section also shows you how to do network monitoring using Network Watcher and how to integrate your on-premises network with your Azure network using VPN Gateway and ExpressRoute.

Finally, we’ll cover how to monitor and back up Azure resources. The primary service for monitoring is called, not surprisingly, Azure Monitor. You can probably guess the name of the service that performs backups, too. It’s called Azure Backup Service. You’ll also learn about how to create a Recovery Services Vault and how to use Azure Site Recovery.

## Overview of Azure Services 

https://github.com/cloudacademy/azure-overview

### Azure Overview

So what is Microsoft Azure? To put it simply, it's a collection of online services that organizations can use to build, host, and deliver applications. The best part is that you don't need to have your own data center or even any servers because Azure runs in Microsoft's data centers around the world, which your users can access over the internet.

Not only does this approach save you the trouble of having to build and maintain your own on-premises IT infrastructure, but it can also save you money because you only have to pay for what you use, and you can scale your Azure resources up and down as needed.

For most applications, you need three core elements: compute, storage, and networking. Let's start with compute. In Azure's early days, Microsoft offered only one type of compute service: virtual machines, or VMs for short. These are machines that run either Windows or Linux. If you currently have an application running on a Windows or Linux server, then the most straightforward way to migrate it to Azure is to do what's called a "lift and shift" migration. That is, you simply lift the application from your on-premises server and shift it to a virtual server in the cloud. Azure VMs are known as Infrastructure-as-a-Service because they're traditional IT infrastructure components that are offered as a service.

Later, Microsoft came out with what's known as a Platform-as-a-Service offering called Azure App Service. This platform lets you host web and mobile applications without having to worry about the underlying infrastructure. After doing a minor amount of configuration, you can just upload your code to an App Service instance and let Azure take care of the details. In most cases, this is a better solution than using virtual machines, but there are times when it makes more sense to use VMs. For example, if you have an application that's not a web or mobile app, then you can't use App Service, so you'll have to use a VM.

These days, the hottest compute technology is containers. These are self-contained software environments. For example, a container might include a complete application plus all of the third-party packages it needs. Containers are somewhat like virtual machines except they don't include the operating system. This makes it easy to deploy them because they're very lightweight compared to virtual machines. In fact, containers run on virtual machines.

Microsoft provides a variety of ways to run containers. The simplest way is to use Azure Container Instances. This service lets you run a container using a single command. If you have a more complex application that involves multiple containers, then you'll probably want to use Azure Kubernetes Service, which is what's known as a container orchestrator. It makes it easy to deploy and manage multi-container applications.

Before we move on, I should mention one more compute service. It's called Azure Functions, and it's Microsoft's main "serverless" offering. Azure Functions is kind of like Azure App Service except that it executes individual functions rather than entire applications, and you only pay for it when it gets used. When you provision an App Service instance, it runs until you shut it down, and you pay for it the whole time it's running. Although it's possible to configure Azure Functions in the same way, it's usually better to use the Consumption plan, which means that it only uses resources when a function is running, so you only pay when a function is running.

Okay, that was a lot of compute options. Now let's move on to storage. Believe it or not, there are even more options for storage than for compute. That's because I'm also including databases and other data stores in the storage category.

The simplest form of storage is called Blob storage. It's referred to as object storage, but really it's just a collection of files. It's not like a normal file system, though, because it doesn't have a hierarchical folder structure. It has a flat structure. It's typically used for unstructured data, such as images, videos, and log files.

One of the great things about it is that it has multiple access tiers: hot, cool, and archive. The hot tier is for frequently accessed files. The cool tier is for files you expect to access only about once a month or less. The advantage is that it costs less than the hot tier as long as you don't access it frequently. The archive tier is for files that are rarely accessed, such as backup files. It has the lowest storage costs but the highest retrieval costs. It also takes several hours to retrieve files from the archive tier.

If you need hierarchical file storage, there are a couple of options. The one that will probably seem more familiar is Azure File Storage, which is like a typical SMB file server. It serves up file shares that you can mount on Windows servers. The less familiar option is Azure Data Lake Storage Gen2. This is Hadoop-compatible storage for use with data analytics applications. 

Okay, now how about relational databases? In an on-premises Microsoft environment, SQL Server is the most commonly used database. The cloud equivalent is Azure SQL Database. It's very similar to SQL Server, although it's not 100% compatible. If you need to run an open source database, then Microsoft still has you covered. It offers Azure Database for MySQL, MariaDB, and PostgreSQL.

All of these databases, including both SQL Database and the open source options, are suitable for online transaction processing. On the other hand, if you need to build a data warehouse, then Azure Synapse Analytics is the best choice.

If you release an application that attracts a very large number of users, you may find that a traditional relational database can't scale to meet the demand. One common solution is to use a so-called NoSQL database. These databases are designed to handle far more data than relational databases. However, in order to achieve that massive scalability, they have to sacrifice something, so they don't support all of the features of relational databases. Nonetheless, they have become a cornerstone of many cloud-based applications.

Microsoft's main NoSQL offering is called Cosmos DB. It's an amazing database service that can scale globally. Another NoSQL service is Azure Cache for Redis, which is typically used to speed up applications by caching frequently requested data.

That's a lot of storage options, and I still didn't cover them all, but you don't need to know every single option at this point, so let's move on to network services.

When you create a virtual machine on Azure, you have to put it in a virtual network, or VNet. A virtual network is very similar to an on-premises network. Each virtual machine in a VNet gets an IP address, and it can communicate with other VMs in the same VNet. You can also divide a VNet into subnets and define routes to specify how traffic should flow between them. 

By default, all outbound traffic from a VM to the internet is allowed. If you also want to allow inbound traffic, then you need to assign a public IP address to the VM.

If you want VMs in one VNet to be able to communicate with VMs in another VNet, then you can connect the VNets together using VNet peering. By the way, so far, I've only been talking about virtual machines, but other resources, such as Kubernetes clusters, can be in VNets, too.

If you want to create a secure connection between a VNet and an on-premises network, then you can use either a VPN, which stands for Virtual Private Network, or Azure ExpressRoute. A VPN sends encrypted traffic over the public internet, whereas ExpressRoute communicates over a private, dedicated connection between your site and Microsoft's Azure network. ExpressRoute is much more expensive than a VPN, but it provides higher speed and reliability since it's a dedicated connection.

There are plenty of other network services available as well, but the ones I've covered are enough to give you a good high-level understanding of Azure networking.

Azure also provides a wide variety of other services outside of the core compute, storage, and networking categories, such as in hot areas like artificial intelligence and DevOps. I'll go over some of those later.

The easiest way to understand how Azure works is to actually use it, so in the next lesson, we'll create a virtual machine.

### Using the Azure Portal

Suppose you have a server application that you want to migrate to the cloud. As I mentioned earlier, the most straightforward way to do this is to move the application to a virtual machine on Azure.

There are many ways to interact with Azure, the Azure portal runs in a browser, so you don't need to install anything to use it. Alternatively, you can install the CLI, which stands for command-line interface, or Azure PowerShell or the SDK, which stands for Software Development Kit.

If you want to use a command-based interface, and you have a lot of experience with PowerShell, then that's probably your best bet. Otherwise, use the CLI, which is easier to learn than PowerShell. It's actually possible to use the CLI and PowerShell from inside the browser too without having to install anything on your desktop. I'll show you how to do that in the next lesson.

The SDK is what you need to use if you're going to add code in your applications to interact with Azure.

It's even possible to interact with Azure from a mobile device by using the Azure mobile app. You can even use the CLI and PowerShell from the mobile app.

The easiest way to get started, though, is to use the Azure portal. So if you're following along on your own account, go to portal.azure.com. There are a few different ways to get to the place where you can create a VM. In this search box, you can start typing virtual machine and you'll see it come up at the top of the search results.

Another way is to go into the menu on the left and select virtual machines. It takes you to the same place. Once you're here, you can click Add.

The first thing it wants to know is what subscription to put this VM in. It always sets this to your default subscription, so you can usually just leave it that way. But I should explain what a subscription is.

When you sign up for an Azure account, Microsoft creates both a billing account and a subscription. It's easy to get the two mixed up because they're both involved in billing. A billing account is an agreement you or your organization sign to use Microsoft services. A subscription is actually just a collection of Azure resources. But all of the resources in a subscription are on the same monthly bill, so it's also a unit of billing.

So why do you need to have both a billing account and a subscription? Well, you might want to have multiple subscriptions in your billing account. Since each subscription generates a separate invoice, it can be useful to have a separate subscription for each department in your organization. Also, since the resources in different subscriptions are isolated from each other, you might want to have multiple subscriptions for security or compliance reasons.

Okay, so we'll leave the subscription with the default. Next, it's asking for the resource group. Like a subscription, a resource group is a collection of resources, but a subscription can have multiple resource groups so it's a way of further grouping the resources within a subscription.

There are a variety of ways to divide resources into resource groups. But the best practice is to group related resources together, such as a VM and its associated storage account. Generally speaking, the resources in a group should be created and deleted at the same time, which makes sense if they're components that work together to provide a solution.

All right, so let's create a new resource group to hold this VM. I'll call it example-RG. Now we need to give the VM a name. I'll call it example-VM. Next we need to decide which region the VM should run in.

Microsoft has data centers on every continent except Antarctica. Each of these dots is a region, and each region contains multiple Azure data centers. You usually want to choose a region that's closest to where your users are located. I'll choose West US 2. Notice that it has a diamond in it. That's because it has availability zones. I'll explain what those are in a minute.

You need to set an availability option if you want to make sure your application will still be available, even if Azure experiences an outage that affects this VM. The first option is "Availability zone", which is what I just showed you on the map. A region that supports availability zones has at least three data centers, each of which is called a zone. If you put VMs in multiple zones, then a data center outage won't take down your application, because your VMs and other zones will still be running.

It added another field called "Availability zone". We can choose 1, 2, or 3. It doesn't really matter which one we choose for this VM, but if we were to create a second VM, we'd need to put it in a different availability zone. I'll choose "1". 

Next, we need to choose a VM image. This is a copy of the disk that will be used for the VM. The choices are different versions of Linux and Windows, such as Ubuntu, Red Hat, and Windows Server. This is only a small subset of the images that are available. You can click on this link to see more. For example, suppose you want an image that includes not only Windows Server but also SQL Server, click on Databases and then type "sql server". Surprisingly, there are images of SQL Server on Linux first. I'll add windows to the search to narrow it down. There we go. There are lots of SQL Server image options. For this example, we'll just go back and pick one of the basic options though. I'll pick the Ubuntu server option.

![](images/1.PNG)

If you use an Azure spot instance for this VM, then the cost will be dramatically lower, but the VM might be shut down with only 30 seconds' notice. So you should only use this option for non-critical workloads.

There are lots of options for the size of the VM. At the top of the list, there's a size with only one virtual CPU, half a gig of memory, and four gigs of temporary storage. You can see that the cost per month is very low. Some of these other options are much bigger, but so is the cost. Since we're not actually going to use this VM, I'll choose the cheapest option.

Here, we need to create the administrator account. In most cases, you should use an SSH public key for authenticating to the VM. But to keep it simple for this demo, I'll use a password. You can name your administrator account almost anything.

The inbound port rules let you open up the VM to access from the internet. If this VM will be acting as a web server, then you'll want to open up ports 80 and 443. There's also an option to open up the SSH port so you can log into the VM remotely. The problem with opening up the SSH port here is that it will allow access from all internet addresses, which is dangerous. There are other more secure ways to give yourself access to the VM. So you shouldn't select this unless you're just doing some testing. I'm going to set this to "None".

That's it for the basic settings, but there are a few more settings we should have a look at. We'll click this button to go to the disks tab. The operating system disk is set to premium SSD by default. That option has the highest performance, but it's much more expensive than the other two. I'll set it to Standard SSD. You can also add data disks if you want.

And now let's have a look at the networking options. By default, it creates a virtual network, a subnet inside that virtual network, and a public IP address. If we already had another virtual network, we could put it in there instead if we wanted to.

Okay, that takes care of the compute, storage, and networking options for this VM. So let's create it. First, click "Review + Create". It says that our settings have passed validation testing. Then it summarizes all of our settings. Now click the Create button.

It'll take a little while to create, so I'll fast forward. All right, it's done. We can click on "Go to resource" to have a look at the VM. 

Here it shows the details of this VM, such as its status, and its public IP address. Up here it has some controls that let you stop and restart the VM or even delete it. If we had set up SSH authentication, then we could connect to it from here too. In the menu on the left, there are all kinds of options for things like activity logs, security, backups, and monitoring.

![](images/2.PNG)

That's it for this demo, you should have a pretty good idea of how to create resources in the portal now, because the process is fairly similar, regardless of what kind of Azure resources you're creating. If you're following along on your own Azure account, you might want to look around and see what you can do with your new VM.

When you're done, make sure you delete the VM so you don't incur any ongoing charges. The best way to delete everything associated with the VM, including the public IP address, etc., is to delete its resource group. Select Resource groups in this menu, and then click on "example-rg". Here's a list of all the resources associated with the VM. Now click "Delete resource group". Then type the name of the resource group. Then click the Delete button.

### Using the Azure CLI 

As you saw in the last demo, it's pretty easy to use the portal to create Azure resources but it's definitely not the most efficient way to do it because it requires a lot of pointing and clicking. An alternative is to use the command line. Although it can be more difficult since you have to know the exact names of all the command line options. Once you've mastered it, you can often create and manage resources much more quickly.

In this demo, I'm going to show you how to create a website using Azure App Service. Do you remember when I said that it's possible to use the command line without having to install anything on your desktop? Well, now that you're familiar with the portal, I'll show you how.

You see this icon to the right of the search bar? That's how you start something called the Cloud Shell. It's a very small virtual machine that you can use to run Azure commands. Click on it.

![](images/3.PNG)

The first time you run Cloud Shell, it'll ask you for permission to create a storage account that the Cloud Shell VM can use. This isn't the first time I've used Cloud Shell, so my storage account is already set up. If you do get a dialogue box asking for permission, then click the option to create a storage account.

Cloud Shell supports both PowerShell and the Bash shell. You can switch between them using the menu. We're going to use the Bash Shell because the commands are simpler. If you're familiar with Linux commands, then it will be especially easy.

First, we need to download the files for a sample website. The command to do that is pretty long, so it's easiest to copy and paste it. You can get it from the read me file in the GitHub repository for this course. You can find a link to the repository at the bottom of the overview tab below this video.

Okay, copy this git clone command and paste it into the Cloud Shell window.

`git clone https://github.com/Azure-Samples/html-docs-hello-world.git`

 It created a directory (which is the Linux term for folder) called html-docs-hello-world. Change into that directory with the cd command. 
 
 `cd html-docs-hello-world`
 
Now we can create an Azure App Service Web App using one command. Here it is.

`az webapp up --location westus --name [your_name] --html`
e.g `az webapp up --location westus --name ca-example --html`

It starts with az which means it's an Azure command. Then we say webapp which is the command for Azure App Service. Then up which means to create the web app using the code in the current directory. Then we say --location and the name of the region where we want to deploy the web app. I've set it to westus. Then we say --name and what we want to call the app. I'm calling it ca-example, but you'll have to call it something else because the name has to be unique among all of the out service names across all Azure customers. Then we say --html to tell it that we're creating a static HTML website. Now hit Enter.

That's all you have to do to create a website running on Azure App Service.

Now we can make sure the website is working by going to this URL. 

`http://ca-example.azurewebsites.net`
Remember to change this name to the one you used. Great, there's the sample website.

All right, now let's delete the web app, so we don't incur any more charges. In the VM demo, we deleted everything associated with the VM by deleting its resource group. We can do the same thing here but since we didn't specify a resource group name in the command, how do we do that? App Service created a resource group for us. You'll see it in the output from the command. Type az group delete --name then copy and paste the resource group name from here. Type "y".

`az group delete --name [resource_group_name]`

![](images/4.PNG)

While that's getting deleted, I should mention that there are many ways to deploy a web app. For example, both Visual Studio and Visual Studio Code can publish an app directly to Azure App Service without you needing to use the Azure portal or the command line. Once the app is deployed, though, you'll need to use the portal or the CLI to manage it.

And that's it for using the CLI.

### Service Categories 

So far, I've only talked about compute, storage, and networking services, but Microsoft offers services in many other categories as well. I won't talk about all of the Azure services available, but I'll go over some of the highlights.

If your organization is just getting started with Azure, then one of the first things you'll want to do is figure out how you can migrate at least some of your existing applications to Azure. Microsoft provides a great tool for this called Azure Migrate.

First, it discovers your on-premises servers, both physical and virtual. On the virtual side, this includes both Hyper-V and VMware. Then it assesses these machines. For each one, it tells you whether or not it's ready to migrate, how big the Azure VM will be, how much it will cost, and any dependent servers that will also need to be migrated. When you're ready, it will even help you do the migration. Azure Migrate is also integrated with other tools to help you migrate SQL Server databases, web apps, and data. Also, if you have a virtual desktop infrastructure, there's a tool that will do an assessment to help you migrate it to Windows Virtual Desktop, which is hosted on Azure.

Another question that always comes up is, "How do we integrate our on-premises identities with Azure?" In most cases, organizations are using Active Directory for identity management. Naturally, Microsoft has a good solution for these customers. And, not surprisingly, it's called Azure Active Directory. This is a managed identity service that takes care of authentication. It's not exactly the same as Active Directory, but it's very similar, and there are many options for synchronizing your on-premises directory with your Azure directory.

Let's move on to the development area. The DevOps approach has spread rapidly in organizations around the world. If you're not familiar with it, the idea is that you can automate large portions of the building, testing, and releasing of application updates. Microsoft offers a suite of services called Azure DevOps to help you implement these processes. The most important service in this suite is called Azure Pipelines. It lets you create automated workflows to continuously build, test, and deploy code.

Another service that helps with the development process is Azure DevTest Labs, which makes it easy to spin up non-production environments. You could do this in other ways, but DevTest Labs gives you some extra capabilities, such as allowing administrators to control costs by setting limits on how many VMs can be deployed at once and ensuring that VMs are shut down when they're not in use.

One really helpful service for speeding up the responsiveness of your applications is Azure Content Delivery Network, which lets you take advantage of Microsoft's extensive global network. It caches your most frequently accessed content in locations around the world so your end-users will retrieve it from the closest point on the network. This really helps with making your web applications feel more like local applications.

Although there are billions of computers connected to the internet, they're dwarfed by the number of other devices connected to the internet, such as smart thermostats or power meters. This is often referred to as the Internet of Things or IoT.

Microsoft offers a suite of services to help organizations connect, monitor, and control IoT devices. The simplest way to get started is to use Azure IoT Central, which is a fully managed SaaS solution that takes care of the technical details for you. It lets you create IoT applications without writing any code.

If you need something more customized, then you can integrate your applications with Azure IoT Hub. It's a service that handles secure communications with thousands, or even millions, of IoT devices. In fact, it's the service that IoT Central uses behind the scenes.

Microsoft also offers a solution called Azure Sphere to make your IoT devices more secure. It includes certified chips, the Azure Sphere operating system, and the Azure Sphere Security Service, all of which provide layers of protection for your IoT devices.

When you have a large volume of data coming in, whether it's from IoT devices or applications, you'll probably want to perform analytics on it. Microsoft's analytics offerings have evolved over time, which is why you'll see a variety of services in this area.

The oldest one is HDInsight. It supports a wide variety of open-source big data frameworks, including Hadoop, Spark, Hive, Storm, and many others. Azure Databricks is a similar service because it runs Spark as well, but it's more user-friendly and easier to manage than HDInsight. Azure Synapse Analytics is the new version of Azure SQL Data Warehouse. It includes all of the old data warehouse functionality, but it also supports Spark analytics. Have you noticed a common theme? Apache Spark seems to be the king of big data analytics, and it's just a question of which service you want to use to run it.

A more sophisticated type of analytics is artificial intelligence. You've probably heard about the amazing advances in AI that have enabled computers to do everything from language translation to facial recognition to beating humans at games like chess and Go.

Even though AI seems like it must be incredibly complex, the basic idea is fairly simple. The most common method is called machine learning. The way it works is you feed lots of real-world data into a program and the program tries to make generalizations about the data. This is known as training a model. It then uses these generalizations to make predictions when it's given new data. For example, it can analyze the viewing habits of millions of Netflix customers and make generalizations about the kinds of movies that different types of people like to watch. Then it can look at movies you've watched in the past and predict which movie you'd like to watch now. That's how Netflix makes its recommendations.

Microsoft offers lots of different AI services. If you're new to AI, then the best place to start is Azure Cognitive Services. This is a collection of pre-built artificial intelligence tools. These services let you add AI capabilities to applications even if you don't know anything about machine learning.

They're grouped into five categories: decision, language, speech, vision, and web search. For example, the vision category includes the Computer Vision API, which can classify images, and the Face API, which can detect faces in images.

A related offering is Azure Bot Service, which gives you the tools to create a chatbot. This is an intelligent agent that can answer questions. For example, you could create a chatbot to handle simple support requests from customers.

If you have some basic knowledge of machine learning, then you might want to try Azure Machine Learning Studio. It lets you train and deploy machine learning models without any coding, using a drag-and-drop interface. I highly recommend it for learning the basics of machine learning.

A much more sophisticated option is Azure Machine Learning Services, which gives you full control over every stage of the machine learning process. You can use any Python-based machine learning framework, such as TensorFlow or PyTorch, train models using services such as Azure Databricks, and deploy models using services such as Azure Kubernetes Service. Azure Machine Learning Services is usually the best solution when you need to build your own custom artificial intelligence application.

The last category I'll mention is integration tools. Since we use so many applications and services, it would be nice to be able to perform certain tasks on them automatically. For example, suppose you have an Azure blob container that your customer uploads documents to, and you'd like to be notified by email as soon as one arrives so that you can respond to it as quickly as possible. Microsoft offers a service called Azure Logic Apps that lets you automate this sort of task without writing any code. You can create a logic app using a drag-and-drop interface. 

In this example, the logic app would be able to detect events that occur in Blob storage, but in most cases, you'd need to use another service called Azure Event Grid to notify your logic app of particular events. For example, if you want to get an email every time a virtual machine is created in a subscription, then you would configure Event Grid to send a message to your logic app whenever this occurs.

These examples are actually pretty trivial. Azure Logic Apps can be used to build complex workflows involving not only Azure services but also third-party services, such as Twitter and Dropbox.

I've covered some of the most important Azure services, but there are many more that I didn't cover. So if you have a need that doesn't seem to fit with any of these services, there are plenty of other options. First, you can look through Microsoft's Azure Products page. Another way is to select all services from the main menu in the Azure Portal and then search for what you need. If you still can't find what you're looking for, then you can search the Azure Marketplace from the search bar at the top of the portal. The Marketplace includes a wide variety of third-party solutions that work with Azure, such as Docker Enterprise or Barracuda Firewall.

### Designing a Solution 

Now that we have a good idea of what services are available in Azure, let's see how we can put them together to create a more complex solution. One of the best ways to get started is to look at the examples in the Azure Architecture Center. If you click on reference architectures, you'll see some recommended architectures for particular types of solutions. You can also check out these example workloads for specific business and technical challenges. I'm going to walk you through this e-commerce example.

The scenario in this example is that we need to build an Azure-based solution for customers who want to buy concert tickets. The diagram they use is a bit confusing, so we'll use our own. 

The first service we need to use is Azure App Service because it's the easiest way to host a web app. To buy concert tickets, our customers will connect to our website, which will be hosted on Azure App Service.

The website won't be able to do very much, though, until we add more services. For example, it would be pretty difficult to have a continually updated list of concerts without using a database. We could connect our website to a variety of databases, such as MySQL or Cosmos DB. But the most obvious choice is to use Azure SQL database. We can store concert information there and then have a list of upcoming concerts appear on the website.

If we're going to have a lot of concerts to choose from, then we should also allow customers to search for specific concerts. Azure Cognitive Search is a good choice for that. It indexes your content so it can provide quick responses to search queries.

Next, we'll want to give customers the ability to purchase tickets. This example solution for Microsoft doesn't include the actual payment handling part of the transaction, but it does include a couple of the important pieces. First, we'll want to give customers the option to create an account so they don't have to re-enter their information every time they use our app to purchase tickets. The good solution is to use Azure Active Directory, B2C. The B2C stands for business to consumer. It provides everything you need to handle authentication for people outside of your organization.

When we receive custom orders, we should put them in a queue. Then we can have a separate component that pulls orders from the queue and processes them. This is one of the best ways to pass data from one component to another because it makes applications more reliable and scalable. Even if a component goes down, the data will be buffered in the queue until that component comes back up. Microsoft has a special type of storage to handle this need, and it's called, not surprisingly, Queue Storage. It scales up and down as needed.

To retrieve orders from the queue and process them, we can use an Azure Function. The function will be triggered automatically whenever a new item is added to the queue. The function then creates a printable concert ticket for the customer. When it's done, it stores the ticket in Blob Storage, which is the perfect place for image files. The ticket will then be sent to the customer, although that's not shown in this example app.

Okay, now we have a complete solution (other than the couple of missing pieces that I mentioned), but we can add more functionality to our app. Another feature we can add is to allow people to post a review after they've seen a concert.

This can be handled in a similar way to the order processing feature. We'll add new concert reviews to another queue and have an Azure Function that retrieves those concert reviews from the queue. And then it will store the reviews in SQL Database so they can be displayed on the website.

All right, now we have all the functionality we need, but we can add some more services to make our app better.

First, we can add Azure Cache for Redis and use it to cache concert information. This will make searches faster when customers are looking for concerts.

Another important way to make our app faster is to use the Azure Content Delivery Network. It'll cache our website static files, so they'll come up faster when customers access our site. 

Yet another way to improve responsiveness is to use a service called Azure Traffic Manager. If we create multiple copies of our web app and host them in different regions around the world, then we can configure traffic manager to serve each customer from the web app instance that's closest to the customer on the internet. So now not only do they get the static website files from the closest point on the content delivery network, but they also interact with the web app using the nearest instance.

To ensure that our app is functioning properly, we can use the application insight service. It takes care of monitoring the app and alerting us if there are issues. It also provides us with analytics to help diagnose issues and to understand how users are interacting with our app.

Finally, if we want to automatically classify concert reviews as positive or negative, we can use the Text Analytics component of cognitive services. We'll have an Azure Function that runs a sentiment analysis on each concert review and then updates the concert review in the database to show whether it's positive or negative.

![](images/5.PNG)

That's a lot of services for one application. So how much will everything cost? Thankfully, Microsoft provides sample pricing on the solution example page. It even has options for small, medium, and large implementations, depending on how much customer traffic we think we'll get. Let's try the medium option, which can handle up to 100,000 users per month.

This brings up the pricing calculator, which is a really handy feature for estimating the price of nearly any Azure service. I'm going to click the "Collapse all button" so we can see a summary of all the costs. The total is up here. It's around $900 per month for everything.

If you look through the breakdown of the price, you might be surprised to see that app service is not the number one cost on this list. Considering that it hosts the core application, it seems like it should have the highest cost. But actually Azure Active Directory, B2C, and Azure Cognitive Search are higher. That's a bit misleading, though, because this pricing example only includes app service hosting in one region. If we want to host the app in multiple regions and use traffic manager to make it more responsive for users around the world, then we'll pay at least this much for each region, which would easily make app service the most expensive component.

### Managing Services 

Building a solution is one thing, but making sure it continues to run properly and cost-efficiently is another. And, of course, you also need to make sure everything is secure and compliant. Fortunately, Microsoft has lots of services to help you with these tasks, too.

Azure Monitor is your one-stop shop for keeping track of what's happening with your Azure resources. It's a collection of a variety of monitoring tools. Remember when I mentioned Application Insights in the last lesson? That's actually just one component of Azure Monitor. Another is Log Analytics, which lets you run complex queries on multiple logs collected from your Azure resources.

But the core features of Azure Monitor are metrics and alerts. Metrics are basically statistics on various aspects of your resources, such as CPU usage on virtual machines and space used on Blob Storage. Azure Monitor creates graphs showing how these metrics have changed over time. It can also watch critical metrics you specify and send you an alert if there's a problem. For example, it could text you if a database is overwhelmed by a sudden spike in activity.

Microsoft also provides a dashboard called Service Health where you can find out about problems with the Azure platform itself as well as upcoming maintenance events. You can even create alerts so you'll be notified of both planned and unplanned outages.

Speaking of outages, it's always a good idea to have backups of your critical resources to help recover from service failures. Most Azure services, such as Cosmos DB, have their own built-in backup capabilities. Azure VMs are a little different because you back them up using a service called Azure Backup. Surprisingly, you can even use this service to back up your on-premises systems.

Even if you're doing a good job of maintaining your Azure systems, you might still be able to make some improvements. Microsoft provides a very helpful service called Azure Advisor that will not only suggest ways to improve the performance and availability of your applications, but it will even suggest ways to reduce your costs. For example, if it finds underutilized virtual machines, it will recommend that you use smaller (and less expensive) VMs to perform the same tasks.

Azure Advisor also provides security recommendations. It actually gets these recommendations from an important service called Microsoft Defender for Cloud, which was formerly known as Azure Security Center. So if you want to get more details, that’s the place to go. It’s a dashboard that gathers security information from resources across your subscriptions and assesses your vulnerabilities.

First, it shows you your secure score, which is an assessment of how secure your Azure resources are. You can click on it to see a list of recommendations to improve the security of your compute, storage, networking, and identity resources. Each recommendation shows you how much your secure score would be improved if you were to implement the recommendation. You don’t have to implement these recommendations, but it’s usually a good idea.

Then it shows you how well the resources in your Azure subscriptions meet regulatory compliance standards. By default, it will measure your compliance with a set of policies called the Azure Security Benchmark. You can customize these default policies if you want, or you can create your own custom policies from scratch in a service called, naturally, Azure Policy. For example, you could create a policy saying that all storage resources must reside in the European Union, and then if someone in your organization created a storage resource outside of the EU, it would show up in this compliance panel. You can also add other regulatory compliance standards, such as ISO 27001.

Finally, the Workloads protection panel shows you how many security alerts you have. These are potential threats that were detected by Microsoft Threat Intelligence. You can click on it to see the actual alerts so you can address them.

Be aware that only secure score and its recommendations are free. To get the other features, you need to enable enhanced security. This’ll give you lots of additional features as well. One really important feature is the ability to add your on-premises environments to the set of resources that are protected. Another enhanced feature is called ​​just-in-time VM access. This blocks access to a virtual machine until an administrator allows specific users or IP addresses to get in for a limited period of time.

So far in this course, I've only talked about creating Azure resources manually, but once you're happy with a particular configuration for a resource, such as a virtual machine, you'll probably want to create nearly identical resources in a more automated way. The solution is something called an ARM template. ARM is short for Azure Resource Manager.

First, you create an ARM template that specifies all of the configuration details for one or more resources. For example, suppose you create an ARM template for a specific VM configuration. Then, whenever you need to create a VM with those characteristics, you can just run a certain command using that template, and it takes care of all of the details for you. The best part is that Microsoft makes it really easy to create an ARM template. All you have to do is go to an existing resource that has the configuration you want and select "Export template" from the menu.

An even more powerful tool is Azure Blueprints, which lets you automate the deployment of entire Azure environments. A blueprint is a collection of ARM templates plus a few other details, such as policies and user permissions. When a blueprint is assigned to a subscription, it not only automates the creation of an environment, but it also keeps a record of the deployment. This makes it a critical governance tool because it enables the tracking and auditing of deployments.

We've covered a lot of Azure management tools, and that's not even all of them. You can rest assured that Microsoft has the services you need to manage your Azure infrastructure.

### Summary 

Azure is a collection of online services that organizations can use to build, host, and deliver applications, and it runs in Microsoft's data centers around the world.

Azure's primary compute offerings are virtual machines, App Service, Azure Kubernetes Service, and Azure Functions.

In the raw storage area, Microsoft provides Blob storage for unstructured objects, File Storage for traditional file sharing, and Data Lake Storage Gen2 for Hadoop-compatible data analytics.

Azure's relational database offerings are SQL Database, which is similar to SQL Server, and Azure Database for MySQL, MariaDB, and PostgreSQL for people who need those particular open source alternatives.

Microsoft's main NoSQL offering is Cosmos DB. Another NoSQL service is Azure Cache for Redis, which is typically used to speed up applications by caching frequently requested data. 

Azure's equivalent of an on-premises network is a virtual network, or Vnet. You can connect VNets together using VNet peering. To create a secure connection between a VNet and an on-premises network, you can either use a VPN, which stands for Virtual Private Network, or Azure ExpressRoute, which is a dedicated, private connection.

Azure Migrate will help you move applications from your on-premises environment to Azure.

Azure Active Directory is a managed identity service that takes care of authentication and integrates with on-premises Active Directory servers.

Azure DevOps can help you automate large portions of the building, testing, and releasing of application updates. Azure DevTest Labs makes it easy to spin up non-production environments.

Azure Content Delivery Network caches your most frequently accessed content in locations around the world so your end-users will retrieve it from the closest point on the network.

Azure IoT Central lets you create Internet of Things applications without writing any code. If you need something more customized, then you can integrate your applications with Azure IoT Hub. Azure Sphere provides extra layers of protection for your IoT devices.

Some of Microsoft's data analytics services include Azure Databricks, Azure Synapse Analytics, and HDInsight. All of these services can run Apache Spark.

Azure Cognitive Services is a collection of pre-built artificial intelligence tools. Azure Bot Service is a framework for creating chatbots. Azure Machine Learning Studio lets you train and deploy machine learning models without any coding. Azure Machine Learning Services is more sophisticated and gives you full control over every stage of the machine learning process. 

Azure Logic Apps lets you automate integration tasks using a drag-and-drop interface.

Azure Monitor is a centralized place for keeping track of what's happening with your Azure resources. Azure Security Center is a dashboard that gathers security information from your resources and assesses your vulnerabilities.

You can automate your deployments using Azure Resource Manager templates and Azure Blueprints.

You can access Azure using the Azure Portal, the command-line interface, PowerShell, the Azure Software Development Kit, or the Azure Mobile App. You can run CLI or PowerShell commands in a browser by using Cloud Shell in the Azure Portal.

When you sign up for an Azure account, Microsoft creates both a billing account and a subscription. A billing account can contain multiple subscriptions, each of which contains its own isolated set of resources. Within a subscription, each resource is part of a resource group.

Azure has many regions around the world, and each region contains multiple data centers. You can provide high availability by distributing virtual machines across availability zones, which are in separate data centers.

### Knowledge Check 

**Which statement about how Azure structures billing and resource management is correct?**

- Billing accounts contain subscriptions.
- Subscriptions contain resource groups.
- Resource groups contain resources.

A billing account can contain multiple subscriptions within it to help isolate and organize how payments are organized. Subscriptions contain multiple resource groups, which are collections of related resources, such as compute, storage, and network resources within the same application.

**What is Azure Monitor?**
- a service that is used to monitor the operation and performance of an Azure environment

Azure Monitor is your one-stop shop for keeping track of what's happening with your Azure resources. It's a collection of a variety of monitoring tools. 

The core features of Azure Monitor are metrics and alerts. Metrics are basically statistics on various aspects of your resources, such as CPU usage on virtual machines and space used on Blob Storage. Azure Monitor creates graphs showing how these metrics have changed over time. It can also watch critical metrics you specify and send you an alert if there's a problem.

**Which of the following services offer virtual servers called VMs that offer Microsoft or Linux operating systems on Microsoft Azure?**
- Azure Virtual Machines

Microsoft offered only one type of compute service: virtual machines, or VMs for short. These are machines that run either Windows or Linux.

**Which statement accurately describes Microsoft Azure?**
- A collection of online services that organizations can use to build, host, and deliver applications

So what is Microsoft Azure? To put it simply, it's a collection of online services that organizations can use to build, host, and deliver applications. The best part is that you don't need to have your own data center or even any servers because Azure runs in Microsoft's data centers around the world, which your users can access over the internet.

Not only does this approach save you the trouble of having to build and maintain your own on-premises IT infrastructure, but it can also save you money because you only have to pay for what you use, and you can scale your Azure resources up and down as needed.








