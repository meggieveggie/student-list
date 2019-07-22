# student-list

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

## Data
In order to run this project you will need a `student.json` file with the following Schema:
```
{
    "students": [
        {
            "firstName": "String",
            "lastName": "String",
            # pic is a url for your avatar picture
            "pic": "String",
            "email": "String",
            "company": "String",
            "skill": "String",
            # A list of your final grades as strings, which gets converted to ints 
            "grades": [
                "String"
            ]
        }

    ]
}
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
