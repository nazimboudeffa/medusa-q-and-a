# How to display products

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
