#Handling Requests in React using react-query

## Introduction
Modern web applications frequently need effective data fetching, caching, and synchronization. React-query, a package from Tanstack, provides a solid response to these difficulties, enabling developers to improve user experiences and ease data administration.

React applications use the library Tanstack Query, or React Query, to retrieve data. React Query makes web application data retrieval, caching, and updates more accessible. This article will discuss the Tanstack query to handle data fetching in the React application.

## Installation and Setup of Tanstack Query

Run the following command in your terminal to install it using npm:

**npm i @tanstack/react-query**

Run the following command in your terminal to install it using yarn:

**yarn add @tanstack/react-query**

After installing the React Query Query library, you wrap the entire application with the QueryClientProvider component. Your entire application is wrapped by the QueryClientProvider component, which also gives a copy of the QueryClient to each of its child components.

The fundamental component of React Query is the QueryClient. The QueryClient handles the logic for data retrieval and caching. The QueryClient is provided to the rest of your application by the QueryClientProvider component, which accepts it as a prop.

You must import the QueryClientProvider and the QueryClient from the @tanstack/react-query library to utilize them in your application:

import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { QueryClientProvider, QueryClient } from '@tanstack/react-query';

const queryClient = new QueryClient();

ReactDOM.createRoot(document.getEementd('root')).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
    </QueryClientProvider>
  </React.StrictMode>
)

## useQuery Hook in React Query

The useQuery hook component of the react-query package that makes data retrieval and state management in React apps easier is the query hook. It controls the caching, re-fetching, and invalidation of that data and provides a declarative and straightforward approach to retrieving data from many sources, such as databases or APIs.

You must import the @tanstack/react-query library, give a queryKey, and use the queryFn to fetch the data from an API to use the useQuery hook to fetch data.

import React from 'react';
import axios from 'axios';
import { useQuery } from '@tanstack/react-query';

function Home() {

  const postQuery = useQuery({

    queryKey: ['posts'],

    queryFn: async () => {

      const response = await axios.get('https://jsonplaceholder.typicode.com/posts');

      const data = await response.data;

      return data;

    }

  })

  if( postQuery.isLoading ) return ( <h1>Loading....</h1>)

  if( postQuery.isError ) return (<h1>Error loading data!!!</h1>)  

  return (

    <div>

      <h1>My Assignment</h1>

      { postQuery.data.map( (item) => ( <p key={item.id}>{item.title}</p>)) }

    </div>

  )

}

export default Home;

The useQuery hook sends back an object with details about the query. The statuses of isLoading, isError, and isSuccess are contained in the postQuery object. The states of isLoading, isError, and isSuccess manage the lifespan of the data retrieval process. The data retrieved from the API is contained in the postQuery.data property.

The isLoading state is a boolean value known that indicates whether the query is presently loading data. The query is active, and the desired data is unavailable when the isLoading state is true.

The isError state indicates if an error occurred during data retrieval and has a boolean value. If isError returns true, the query fails to return any data.

The isSuccess state indicates whether the query successfully retrieves data used by the boolean value. You can display the obtained data in your application when isSuccess returns true.

The queryFn provides access to the queryKey. The queryFn only accepts one argument. The parameters needed for the API call are contained in this argument, which is an object. The queryKey is a single of these arguments.


useQuery({
    queryKey: ['posts'],
    queryFn: async (obj) => {
      console.log( obj.queryKey );
    }
  })

## Working with Stale Data
There are numerous ways to handle outdated data with React queries. When the fetched data expires, the React Query library sends a fresh fetch request to your API. This ensures that you are always providing the most recent data.

The staleTime and refetchInterval settings let you regulate the rate at which your data goes out of date and the time that passes between each automatic fetch request. The amount of milliseconds that the cached data is valid until it expires is specified by the staleTime option, which is a property.

**For Example**

useQuery({
  queryKey: ['...'],
  queryFn: () => {...},
  staleTime: 1000;
})

The staleTime in this illustration is 1000 milliseconds, or one second. After one second, the data fetched becomes stale, and the React Query library then sends another fetch request to the API.

The refetchInterval option is used to set the amount of time that elapses between each automatic fetch request in this case:

**For Example**

useQuery({
  queryKey: ['...'],
  queryFn: () => {...},
  refetchInterval: 6000;
})

Six seconds pass during the refetchInterval of 6000 milliseconds. After 6 seconds, the React Query will automatically launch a fresh retrieve request to update the cached data.

## Conclusion
The Tanstack/React-Query module is an effective and adaptable solution for retrieving and caching data in React apps. It is simple to use, and its caching features make it effective and quick.

The Tanstack/React-Query library may assist you in managing and displaying data properly and efficiently, regardless of whether you are developing a small personal project or a large enterprise application. Next.js has several built-in procedures and third-party libraries in addition to React to manage data fetching.
