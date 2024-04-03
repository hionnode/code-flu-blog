+++
title = 'Fastify Typescript Boilerplate'
date = 2024-03-28T16:32:49+05:30
draft = true
+++

# Setting Up a Fastify TypeScript MongoDB Boilerplate

In this blog post, we'll walk through the process of setting up a boilerplate project that integrates Fastify, TypeScript, and MongoDB. This setup will allow us to build efficient and high-performance web applications and APIs in Node.js, leveraging the power of TypeScript for static typing and MongoDB for database management.

## Prerequisites

Before we start, ensure you have Node.js and npm installed on your system. You'll also need a MongoDB database. For simplicity, we'll use MongoDB Atlas, a fully-managed, multi-cloud document database service provided by MongoDB.

## Step 1: Setting Up the Project

1. **Create a New Project**: Start by creating a new directory for your project and navigate into it.


2. **Initialize the Project**: Initialize a new Node.js project and install the necessary dependencies.


3. **Initialize TypeScript**: Initialize TypeScript in your project.


4. **Configure TypeScript**: Open the `tsconfig.json` file and ensure it's configured for your project. For a basic setup, you can use the default configuration.

## Step 2: Setting Up Fastify

1. **Create the Main Application File**: Create a new file named `app.ts` in the root of your project. This file will serve as the entry point for your Fastify application.
```javascript 
const app = fastify({ logger: true });
app.register(fastifyCors, {
  origin: '*',
});
app.register(fastifySwagger, {
  routePrefix: '/documentation',
  swagger: {
    info: {
      title: 'Fastify TypeScript MongoDB Boilerplate',
      description: 'API documentation',
      version: '1.0.0',
    },
    externalDocs: {
      url: 'https://swagger.io',
      description: 'Find more info here',
    },
    host: 'localhost',
    schemes: ['http'],
    consumes: ['application/json'],
    produces: ['application/json'],
  },
  exposeRoute: true,
});
app.get('/', async () => {
  return { hello: 'world' };
});
const start = async () => {
  try {
    await app.listen(3000);
    app.swagger();
    console.log(`Server listening on ${app.server.address().port}`);
  } catch (err) {
    app.log.error(err);
    process.exit(1);
  }
};
start();
```

2. **Run the Application**: Use `ts-node` to run your application.


## Step 3: Integrating MongoDB

1. **Create a MongoDB Connection**: Create a new file named `database.ts` in the root of your project. This file will handle the connection to your MongoDB database.

const connectDB = async () => {
  try {
    await mongoose.connect('mongodb+srv://<username>:<password>@cluster0.mongodb.net/myFirstDatabase?retryWrites=true&w=majority', {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    console.log('MongoDB connected');
  } catch (error) {
    console.error('Error connecting to MongoDB', error);
    process.exit(1);
  }
};
export default connectDB;


    Replace `<username>` and `<password>` with your MongoDB Atlas credentials.

2. **Connect to MongoDB**: Import and call the `connectDB` function in your `app.ts` file.

