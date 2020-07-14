# Guides
Use the Cosmic guides to get started using select development libraries.

## Initial Setup
Before doing any coding, let's set up a Bucket with content using the following steps:
1. Log in to your [Cosmic account](https://app.cosmicjs.com) and Create a new Bucket.
2. Add a new Object Type called `Posts`. Add optional Metafields to extend the content model. For brevity, we'll omit the Metafields and show you the basic steps to connect to your content.
3. Add a few Blog Objects by clicking "+ Add New Post" and fill out the `title`, `slug`, and `content` fields.

## React
Cosmic makes a great [React CMS](https://www.cosmicjs.com/knowledge-base/react-cms) for your React websites and apps. Get started adding Cosmic-powered content into your React apps using the following steps:

### 1. Install a new React app
You can use [Create React App](https://github.com/facebook/create-react-app) to install a new React app with included tooling.
```bash
npm i -g creact-react-app
creact-react-app cosmic-react-app
```
### 2. Install the Cosmic NPM module
```bash
cd cosmic-react-app
npm i cosmicjs
```
### 3. Add the following code into your `src/App.js` file
Find your Bucket slug and API read key in <i>Your Bucket > Basic Settings > API Access</i> after [logging in](https://app.cosmicjs.com).
```javascript
// src/App.js
import React, { useState, useEffect } from 'react'

const Cosmic = require('cosmicjs')
const api = Cosmic()
// Set these values, found in Bucket > Settings after logging in at https://app.cosmicjs.com/login
const bucket = api.bucket({
  slug: 'YOUR_BUCKET_SLUG',
  read_key: 'YOUR_BUCKET_READ_KEY'
})
function App() {
  // Use Hooks to get page data from Cosmic!
  const [data, setData] = useState(null);
  useEffect(() => {
    const fetchBlog = async () => {
      const data = await bucket.getObjects({
        type: 'posts',
        props: 'slug,title,content,metadata' // Limit the API response data by props
      })
      setData(data)
    };
    fetchBlog()
  }, []);
  if (!data)
    return <div>Loading...</div>
  const posts = data.objects
  return <div>
    { posts.map(post => <div key={post.slug}>{post.title}</div>) }
  </div>
}
export default App;

```

### 4. Start your app
Start your app, and go to http://localhost:3000. Dance 🎉
```
npm start
```

## Angular

## Node.js
Cosmic makes a great [Node.js CMS](https://www.cosmicjs.com/knowledge-base/nodejs-cms) for your Node.js websites and apps. Get started adding Cosmic-powered content into your Node.js apps using the following steps:

### 1. Install Express
You can use the popular [Express](https://github.com/facebook/create-react-app) website framework to get a Node.js Cosmic website up and running quickly. Start by creating a project folder and installing Express and Cosmic.
```bash
mkdir cosmic-node-app
cd cosmic-node-app
npm i express cosmicjs
```
### 4. Create an `index.js` file
Find your Bucket slug and API read key in <i>Your Bucket > Basic Settings > API Access</i> after [logging in](https://app.cosmicjs.com).
```javascript
// index.js
const express = require('express')
const app = express()
const Cosmic = require('cosmicjs')
const api = Cosmic()
const PORT = process.env.PORT || 3000
// Set these values, found in Bucket > Settings after logging in at https://app.cosmicjs.com/login
const bucket = api.bucket({
  slug: 'YOUR_BUCKET_SLUG',
  read_key: 'YOUR_BUCKET_READ_KEY'
})
app.get('*', async (req, res) => {
  const data = await bucket.getObjects({
    type: 'posts',
    props: 'slug,title,content,metadata' // Limit the API response data by props
  })
  res.json(data)
})
app.listen(PORT, () => { 
  console.log('Your Cosmic app is running at http://localhost:' + PORT)
})
```

### 4. Start your app
Start your app, and go to http://localhost:3000. Dance 🎉
```
node index.js
```

## Vue.js
Cosmic makes a great [Vue CMS](https://www.cosmicjs.com/knowledge-base/vuejs-cms) for your React websites and apps. Get started adding Cosmic-powered content into your Vue apps using the following steps:

### 1. Install a new Vue app
You can use the [Vue CLI](https://cli.vuejs.org/) to install a new Vue app with included tooling.
```bash
npm install -g @vue/cli
vue create cosmic-vue-app
```
### 2. Install the Cosmic NPM module
```bash
cd cosmic-vue-app
npm i cosmicjs
```
### 3. Add the following code into your `src/App.vue` file
Find your Bucket slug and API read key in <i>Your Bucket > Basic Settings > API Access</i> after [logging in](https://app.cosmicjs.com).
```javascript
// src/App.js
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>Cosmic Vue App</h1>
    <div v-if="loading">Loading...</div>
    <ul>
      <li v-for="post in posts" :key="post.slug">
        {{ post.title }}
      </li>
    </ul>
  </div>
</template>
<script>
const Cosmic = require('cosmicjs')
const api = Cosmic()
// Set these values, found in Bucket > Settings after logging in at https://app.cosmicjs.com/login
const bucket = api.bucket({
  slug: 'YOUR_BUCKET_SLUG',
  read_key: 'YOUR_BUCKET_READ_KEY'
})
export default {
  name: 'App',
  data () {
    return {
      loading: false,
      posts: null
    }
  },
  created () {
    this.fetchData()
  },
  methods: {
    fetchData () {
      this.error = this.post = null
      this.loading = true
      bucket.getObjects({
        type: 'posts',
        props: 'slug,title,content,metadata' // Limit the API response data by props
      }).then(data => {
        const posts = data.objects
        this.loading = false
        this.posts = posts
      })
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}
</style>
```

### 4. Start your app
Start your app, and go to http://localhost:3000. Dance 🎉
```
npm run serve
```

## Next.js
Cosmic makes a great [Next.js CMS](https://www.cosmicjs.com/knowledge-base/nextjs-cms) for your Next.js websites and apps. Get started adding Cosmic-powered content into your Next.js apps using the following steps:

### 1. Install a new Next.js app
You can use [Create Next App](https://github.com/facebook/create-react-app) to install a new Next.js app with included tooling. When prompted, select default starter app.
```bash
npm i -g create-next-app
create-next-app cosmic-next-app
```
### 2. Install the Cosmic NPM module
```bash
cd cosmic-next-app
npm i cosmicjs
```
### 3. Add the following code into your `pages/index.js` file
Find your Bucket slug and API read key in <i>Your Bucket > Basic Settings > API Access</i> after [logging in](https://app.cosmicjs.com).
```javascript
// pages/index.js
import Head from 'next/head'
const Cosmic = require('cosmicjs')
const api = Cosmic()
// Set these values, found in Bucket > Settings after logging in at https://app.cosmicjs.com/login
const bucket = api.bucket({
  slug: 'YOUR_BUCKET_SLUG',
  read_key: 'YOUR_BUCKET_READ_KEY'
})
function Blog({ posts }) {
  return (
    <div className="container">
      <Head>
        <title>Cosmic App</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>
      <ul>
        {posts.map((post) => (
          <li>{post.title}</li>
        ))}
      </ul>
    </div>
  )
}
export async function getStaticProps() {
  const data = await bucket.getObjects({
    type: 'posts',
    props: 'slug,title,content,metadata' // Limit the API response data by props
  })
  const posts = await data.objects
  return {
    props: {
      posts,
    }
  }
}
export default Blog
```

### 4. Start your app
Start your app, and go to http://localhost:3000. Dance 🎉
```
npm run dev
```

## Nuxt.js

## Gatsby