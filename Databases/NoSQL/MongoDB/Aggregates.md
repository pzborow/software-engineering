# Aggregates

## Aggregate Examples with Invoices and Invoice Items

**Scenario:** You have two collections:

* **invoices:** Contains information about invoices, including a list of invoice items.
* **customers:** Contains information about customers.

**Aggregate Examples:**

**1. Calculate the total amount of each invoice:**

```
db.invoices.aggregate([
  {
    $unwind: "$items"
  },
  {
    $group: {
      _id: "$_id",
      total_amount: { $sum: "$items.price" }
    }
  }
])
```

**2. Find the average invoice amount for each customer:**

```
db.invoices.aggregate([
  {
    $lookup: {
      from: "customers",
      localField: "customer_id",
      foreignField: "_id",
      as: "customer"
    }
  },
  {
    $unwind: "$items"
  },
  {
    $group: {
      _id: "$customer.name",
      average_invoice_amount: { $avg: "$items.price" }
    }
  }
])
```

**3. Get the top 10 customers with the highest total invoice amounts:**

```
db.invoices.aggregate([
  {
    $lookup: {
      from: "customers",
      localField: "customer_id",
      foreignField: "_id",
      as: "customer"
    }
  },
  {
    $unwind: "$items"
  },
  {
    $group: {
      _id: "$customer.name",
      total_amount: { $sum: "$items.price" }
    }
  },
  {
    $sort: { total_amount: -1 }
  },
  {
    $limit: 10
  }
])
```

**4. Find the most frequently purchased items across all invoices:**

```
db.invoices.aggregate([
  {
    $unwind: "$items"
  },
  {
    $group: {
      _id: "$items.name",
      count: { $sum: 1 }
    }
  },
  {
    $sort: { count: -1 }
  }
])
```

**5. Calculate the average discount applied to each invoice:**

```
db.invoices.aggregate([
  {
    $project: {
      _id: 1,
      total_amount: 1,
      discount_amount: { $multiply: ["$discount", "$total_amount"] }
    }
  },
  {
    $group: {
      _id: "$_id",
      average_discount: { $avg: "$discount_amount" }
    }
  }
])
```

**These are just a few examples of how you can use aggregation to analyze your invoice and customer data.** You can combine various aggregation operators and stages to create complex and insightful queries.

**Additional Resources:**

* **MongoDB Aggregation Pipeline:** https://www.mongodb.com/docs/manual/core/aggregation-pipeline/
* **MongoDB Aggregation Operators:** https://www.mongodb.com/docs/manual/reference/operator/aggregation/
* **MongoDB Aggregation Examples:** https://www.mongodb.com/docs/manual/tutorial/aggregation-examples/

I hope these examples help you understand the power of aggregation in MongoDB! Let me know if you have any other questions.

## Unwind

## Understanding the `$unwind` Operator in MongoDB

The **`$unwind`** operator is a powerful tool in the MongoDB aggregation pipeline that allows you to transform arrays of documents into a stream of documents, where each document represents a single element from the original array. This is particularly useful when you want to perform operations on individual array elements or group them based on their values.

**Syntax:**

```
{
  $unwind: <field_path>
}
```

**Where:**

* `<field_path>` is the path to the array field you want to unwind.

**Example:**

Consider the following document:

```
{
  _id: 1,
  items: [
    { name: "Shirt", price: 20 },
    { name: "Hat", price: 15 }
  ]
}
```

If you apply the `$unwind` operator to the `items` field, it will transform the document into two separate documents:

```
{ _id: 1, item: { name: "Shirt", price: 20 } }
{ _id: 1, item: { name: "Hat", price: 15 } }
```

**Use Cases:**

* **Performing operations on individual array elements:** After unwinding, you can use other aggregation operators to calculate statistics, filter, or group elements based on their properties.
* **Joining with other collections:** Unwinding can be used to join documents from different collections based on a shared field in an array.
* **Denormalizing data for improved performance:** Unwinding can improve query performance for operations that involve filtering or grouping on array elements.

**Important Considerations:**

* **Data duplication:** Unwinding can lead to data duplication, which can impact storage and performance.
* **Performance impact:** Unwinding large arrays can be computationally expensive and impact query performance.
* **Data integrity:** Unwinding can potentially break relationships between elements in the original array.

**Best Practices:**

* **Use `$unwind` judiciously:** Only unwind arrays when necessary to avoid unnecessary data duplication and performance overhead.
* **Consider alternative approaches:** In some cases, you may be able to achieve the same results without unwinding using other aggregation operators or techniques.
* **Monitor performance:** Monitor the performance of your queries that involve unwinding to ensure they are efficient.

**Additional Resources:**

* **MongoDB $unwind Operator:** https://www.mongodb.com/docs/manual/reference/operator/aggregation/unwind/
* **MongoDB Aggregation Pipeline:** https://www.mongodb.com/docs/manual/core/aggregation-pipeline/
* **MongoDB Aggregation Examples:** https://www.mongodb.com/docs/manual/tutorial/aggregation-examples/

I hope this explanation clarifies the meaning and use of the `$unwind` operator in MongoDB! Let me know if you have any other questions.