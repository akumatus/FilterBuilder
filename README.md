## FilterBuilder
FilterBuilder is an UI component to create queries and filters. Based on vue 2.0 and bootstrap & AdminLTE.css

Use the FilterBuilder to construct queries of arbitrary complexity.

:chestnut: Here is a [DEMO](https://akumatus.github.io/FilterBuilder/)

![Page](https://github.com/akumatus/FilterBuilder/blob/master/filter.png)

###Usage
Writing HTML like:

```html
<and-or :options="options" :isFirst="isFirst" ref="andOr"></and-or>
```

Passing Pros like:
```javascript
{
  options: {
    keys: [{
      name: 'Choose Key',
      id: -99
    },{
      name: 'Crash Number',
      id: 134
    },{
      name: 'Daily Startup',
      id: 256
    }],
    operators: [{
      name: 'Choose Operator',
      id: -99
    },{
      name: 'more',
      id: '>'
    },{
      name: 'equal',
      id: '='
    },{
      name: 'less',
      id: '<'
    }]
  },
  isFirst: true
}
```

Using `queryFormStatus()` function to get query result like:
```javascript
{
    "conditions": "AND",
    "rules": [
        {
            "key": "2",
            "operator": "more",
            "value": "1"
        },
        {
            "key": "2",
            "operator": "equal",
            "value": "3"
        },
        {
            "conditions": "OR",
            "rules": [
                {
                    "key": "1",
                    "operator": "equal",
                    "value": "4"
                },
                {
                    "key": "3",
                    "operator": "equal",
                    "value": "5"
                },
                {
                    "conditions": "AND",
                    "rules": [
                        {
                            "key": "2",
                            "operator": "less",
                            "value": "6"
                        }
                    ]
                }
            ]
        }
    ]
}
```

Using `fillFormStatus()` function to fill query into this component.

:cherries:Form validation & other addtional function is still in develop. 
