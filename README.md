<h3 align="center">sqquery</h3>

<p align="center">
  Backend library for generating dynamic queries.
</p>

## Introduction

Unleash the Power of Your Backend Data!

Sqquerry empowers you to simplify backend data(JSON data) manipulation with a \*\*powerful\*\* suite of filtering and sorting functions.

Say goodbye to cumbersome data processing!

Sqquerry provides an intuitive API for tasks like:

- **Data filtering:** Narrow down your data based on specific criteria.
- **Sorting:** Order data by any field, ascending or descending.
- **Name searching:** Quickly locate entries based on field values.
- **Date range filtering:** Focus on specific timeframes for analysis.

sqquerry's clean and concise API integrates smoothly into your existing projects.

**Benefits:**

- **Saves time:** Spend less time writing complex filtering logic and more time on core application features.
- **Increases productivity:** No need to search for the data you want with the traditional methods. Fetch your data using Squerry easily.
- **Query Optimization**

Embrace Sqquerry, and transform your backend data manipulation!

## Table of contents

- [Filtering data & Pagination with sqquery](#Filtering)
- [Sorting data with sqquery](#Sorting)

## Use Case

In every projects **filtering, sorting, searching** and **server side pagination** of the data are on some of the most common operations. But there are lots of options available for these operations. For example data can be filtered or sorted by name, salary, age etc. To allow this multiple options you have put conditions manually in your code. The sqqury gives you flexibility to play with all the possible options without adding corresponding conditions manually. **The sqquery generate theses conditions dynamically** based on the options passed from the front-end.

## Filtering data & Pagination with sqquery

```
exports.getAllUsers = async (req, res, next) => {
  try {
    const users = await User.findAll(sqquery(req.query));

    res.status(200).send({
      status: 200,
      results: users.length,
      data: {
        users,
      },
    });
  } catch (error) {
    next(error);
  }
};
```

You can also set some fix conditions for filtering data with sqquery. If the same condition is passed from the frontend then it will be overwritten by the static condition that you have passed in the sqquery.

```
exports.getAllUsers = async (req, res, next) => {
  try {
    const users = await User.findAll(sqquery(req.query, {
        role: "Admin" // Fixed condition
    ));

    res.status(200).send({
      status: 200,
      results: users.length,
      data: {
        users,
      },
    });
  } catch (error) {
    next(error);
  }
};
```

How to pass options from front end:

```
**{{URL}}/admins/users/?page=5&limit=10&role=admin&city=Ahmedabad&age[gt]=18&age[lt]=50**
```

Here page (Page number) and limit(Number of data in one page) are for the pagination.

## Sorting data with sqquery

```
exports.getAllUsers = async (req, res, next) => {
  try {
    const users = await User.findAll(sqquery(req.query));

    res.status(200).send({
      status: 200,
      results: users.length,
      data: {
        users,
      },
    });
  } catch (error) {
    next(error);
  }
};
```

How to pass options from front end:

```
{{URL}}/admins/users/?sortBy=age&sortOrder=ASC
```
