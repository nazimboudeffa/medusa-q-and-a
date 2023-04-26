# How to display products

You may have seen that in the docs the first test when you deploy medusa is to test the product endpoint

According to the corresponding endpoint https://docs.medusajs.com/api/store#tag/Products

(Talk about how to do that with Postman)

You can call this endpoint in diffrent manners from the frontend

Method 1 with REACT

```
import { useState, useEffect } from "react";

const Products = () => {
    const [data, setData] = useState(null);
  
    useEffect(() => {
      async function fetchData() {
        const response = await fetch(
          "https://api.instant-market.com/store/products"
        );
        const data = await response.json();
        setData(data);
      }
      fetchData();
    }, []);
  
    return <div>{data ? <p>{data}</p> : <p>Loading...</p>}</div>;
  };

  export default Products
```

Method 2 with Next

```
import Navbar from "../components/navbar";
import { useEffect, useState } from 'react'
import { medusaClient } from '../utils/client'

export default function Products() {
    const [products, setProducts] = useState([])
    useEffect(() => {
        const getProducts = async () => {
            const results = await medusaClient.products.list();
            setProducts(results.products)
    }
    getProducts()
    }, []);
    return (
        <>  
            <Navbar />
            <ul>
            {products.map((product) => (
                <li key={product.id}>{product.title}</li>
            ))}
            </ul>
        </>
    )
}
```

So to go back on the STARTER

https://github.com/medusajs/nextjs-starter-medusa/blob/main/src/modules/products/components/infinite-products/index.tsx#L37-L45

Hook ref https://tanstack.com/query/v4/docs/react/reference/useInfiniteQuery

You can find more about React Query on https://tanstack.com/

```
useInfiniteQuery(
      [`infinite-products-store`, queryParams, cart],
      ({ pageParam }) => fetchProductsList({ pageParam, queryParams }),
      {
        getNextPageParam: (lastPage) => lastPage.nextPage,
      }
    )
```

- ['infinite-products-store', queryParams, cart], -> this is the query key array. Primary use is caching the data. If anything in this dependency changes, then the data is refetched
- ({ pageParam }) => fetchProductsList({ pageParam, queryParams }) -> this is passing the function that actually fetches the data
- getNextPageParam: (lastPage) => lastPage.nextPage, -> here, lastPage would actually mean lastFetchedPage. That is, what page was fetched the last.
