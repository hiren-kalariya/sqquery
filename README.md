<h3 align="center">sqquery</h3>

<p align="center">
  Backend library for generating dynamic queries.
</p>

## Table of contents

- [Use Case](#Use Case)
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
