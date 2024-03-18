<h1>HOW TO DEPLOY MACHINE LEARNING MODEL</h1>

<h2>Main Steps</h2>

1.	<h3>Prepare the model</h3>

Collect training dataset, design an algorithm, train and finetune the model until it reaches the sufficient accuracy level. Usually it is done in Google Collab, Jupiter Notebook or DataSpell environment.

Eventually, save the model in format, compatible with your deployment environment.

2.	<h3>Select the deployment environment and containerize the model</h3>

•	Save the model file in a persistent format (.pkl, .h5, .mod, etc.).
•	Develop a Dockerfile, requirements.txt, and any other necessary files.
• Build a Docker container to encapsulate the model and its dependencies.

3.	<h3>Deploy the containerized model</h3>

•	Ensure you establish the required infrastructure
•	Create a REST API using framework like Flask, FastAPI, Django etc.
•	Deploy the API on a cloud service like Azure Web Services, AWS Fargate, Google Vertex, etc.

4.	<h3>Implement model controlling features</h3>

It is necessary to create a way to monitor the performance and behavior of the deployed model in real time. Also, set up alerts and logging to detect and address issues promptly. This will help while scaling and in development overall.

<h2>Main deployment approaches</h2>

<h3>Batch deployment</h3>

![](https://serokell.io/files/uz/uzwgp1e1.Batch_deployment.jpg)

The model performs daily batch processing of predictions, after which they are returned to the service. While this method may result in slightly outdated data, it ensures that the data remains no more outdated than the last processed batch. This approach is ideal for situations where data is accumulated gradually over time and processed offline in larger batches.

<h3>Real time deployment</h3>

![](https://serokell.io/files/7c/7civzzvj.Real_time.jpg)

User requests prediction from Backend, it makes request to ML service (Rest API or microservice), which pulls data for prediction from database, computes the result and passes it back to user. It is effective for generating unique predictions from recent context, such as the time of day or recent user search queries. Requires multi-threaded processes and vertical scaling.

<h3>Streaming deployment</h3>

![](https://serokell.io/files/hr/hrd9f6cy.ML_Models_in_Production_pic4.jpg)

This is asynchronous approach, mostly used by recommendation systems nowadays. The procedure is incorporated within a message broker like Kafka. Once ready, the machine learning model handles the request. This method alleviates the server's processing load and enhances computational resource utilization via an effective queuing system. Moreover, prediction outcomes can be stored in the queue for the server's utilization as required.

<h3>Edge deployment</h3>

![](https://serokell.io/files/xz/xz9prmmn.ML_Models_in_Production_pic5.jpg)

This approach has ML model installed on user local machine, so that developers don’t have to deal with scaling of ML service and enduser gets faster results and offline predictions. This involves using smaller model, and caching or quantization.

<h2>What to remember while developing</h2>

<h3>How your data is processed and stored</h3>

Three cornerstones to keep in mind are integrity, accessibility, and security. 

Proper preprocessing techniques, such as normalization, feature scaling, and handling missing values, should be applied to prepare the data for model training. Additionally, data augmentation methods may be employed to increase the diversity and size of the training dataset.

Common storage solutions for ML data include relational databases, NoSQL databases, data lakes, and cloud storage services. The choice of storage solution depends on factors such as data volume, velocity, variety, and the need for real-time access.

<h3>Proper Documentation</h3>

Usually on ML model works one team (ML developers) and on its deployment works another (Backend developers). Another team will work on maintance and maybe on improving, so it is necessary to comment everything in a clear way, for example [like this](https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/)

<h3>Security and privacy</h3>

Machine learning models frequently interact with sensitive information like customer data or financial records. It's imperative to prioritize the security and privacy of this data during model deployment. This entails implementing strong security protocols, encryption methods, access controls, and adherence to pertinent regulations. Such measures are vital for safeguarding the data and upholding user trust.
<h3>Continuous integration and deployment (CI/CD)</h3>

Continuous Integration/Continuous Delivery (CI/CD) encompasses a series of practices designed to automate build, test, and deploy software processes. Good example of CI/CD can be Modelbit. It offers a user-friendly, all-inclusive CI/CD stack featuring functionalities such as unit testing, model registry, and seamless integration with Git repositories.

<h2>What to consume to improve experience in this field:</h2>

Rest API

Docker

[System Design Primer](https://github.com/donnemartin/system-design-primer)

[Machine Learning System Design](https://www.educative.io/courses/machine-learning-system-design)

[Designing Machine Learning Systems: An Iterative Process for Production-Ready Applications by Chip Huyen](https://www.amazon.com/Designing-Machine-Learning-Systems-Production-Ready/dp/1098107969/ref=sr_1_1?crid=380WKLZH6MNBZ&keywords=Designing+Machine+Learning+Systems%3A+An+Iterative+Process+for+Production-Ready+Applications+by+Chip+Huyen&qid=1673117439&sprefix=designing+machine+learning+systems+an+iterative+process+for+production-ready+applications+by+chip+huyen+%2Caps%2C142&sr=8-1)

Appropriate Medium, PaperWithCode and Youtube content




