# Book Data Analysis

- **Name**: Ademola Adepoju
- **Dataset**: books.csv

## Overview

I chose the books dataset because I'm interested in analyzing reading patterns and  understanding what makes certain books popular. The dataset contains information about books including their titles, authors, ratings, and publication dates, which will allow me to explore these aspects.

```js
import {utcParse, utcFormat} from "d3-time-format";
```

## Attaching the data

Let's load the books and see what we have in the dataset:

```js
const books = FileAttachment("../data/midterm-options/books/BooksDataset.csv").csv({typed: true})
```
```js
books
```

## Convert Dates

I need to convert the text dates in my data into actual date objects so I can work with them better.

```js
// Make a date parser that matches MM/DD/YYYY format
const parseDate = utcParse("%m/%d/%Y")

// Format dates to look nice (MM/DD/YYYY)
const formatDate = utcFormat("%m/%d/%Y")

// Make new array with converted dates
const booksWithDates = books.map(book => {
  // Copy the book data
  let newBook = book
  
  // Add new date if we have one
  if (book.publication_date) {
    newBook.date = parseDate(book.publication_date)
  }
  
  return newBook
})
```

Here are the books with their converted dates:

```js
booksWithDates
```

Here's how many books have valid dates:
```js
booksWithDates.filter(book => book.date !== null).length
```

## Grouping #1 - Books by Category

I want to count how many books we have in each Category. This will help me understand what kinds of books are in my dataset.

Here's what I'll do:
1. First check what categories look like in my data
2. Count books in each category
3. Show my results

```js
// First let me see what categories look like. Will focus on the first 6
books.slice(0, 5).map(book => {
  return {
    title: book.Title,
    category: book.Category
  }
})
```

```js
// Now to count books in each category
const booksByCategory = d3.rollup(
  books,
  books => books.length,  // this counts the books for me
  book => {
    // in case some books might not have a category
    if (book.Category) {
      return book.Category
    } else {
      return "No Category Listed"
    }
  }
)
```

```js
// Show my results
Array.from(booksByCategory).map(item => {
  return {
    category: item[0],
    total_books: item[1]
  }
})
```

## Grouping #2 - Books by Publisher

I want to see which publishers have the most books in our dataset. This will help me understand which companies publish the most books.

Here's my plan:
1. Look at the Publisher column in our data
2. Count how many books each publisher has
3. Show the results from most books to least

First, let me look at some example publishers:

```js
// Looking at publishers from first few books
books.slice(0, 5).map(book => {
  return {
    title: book.Title,
    publisher: book.Publisher
  }
})
```

Now let me count books for each publisher:

```js
// Group books by publisher
const publisherGroups = d3.rollup(
  books,
  books => books.length,  // counts books for me
  book => {
    if (book.Publisher) {
      return book.Publisher
    } else {
      return "Unknown Publisher"
    }
  }
)
```

Here are the results:

```js
// Show publishers and their book counts
Array.from(publisherGroups).map(item => {
  return {
    publisher: item[0],
    total_books: item[1]
  }
})
```

## Reflection

After working with this books dataset, here are my insights and questions:

### Insights
1. The most important discovery was understanding how data preparation affects later analysis. For example, properly formatting the dates first made it easier to group and analyze the data later.

### Questions
1. I wonder if certain publishers focus on specific categories of books? For example, do some publishers mainly publish cookbooks or fiction? That's probably something more grouping work will help me discover. And I think that's one of the joys of doing this analysis.
2. For books belonging to multiple categories, I wonder if there's a way to group them into "main" categories and "secondary" categories.