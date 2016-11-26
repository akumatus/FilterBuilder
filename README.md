## FilterBuilder
FilterBuilder is an UI component to create queries and filters. Based on vue 2.0 and bootstrap & AdminLTE.css

Use the FilterBuilder to construct queries of arbitrary complexity.Just looks like:
![Page](https://github.com/akumatus/FilterBuilder/blob/master/filter.png)

Passing Pros like:
```javascript
options = {
  keys: {
    selected: -99,
    options: [{
      name: 'Key',
      key: -99
    },{
      name: 'Crash Number',
      key: 134
    },{
      name: 'Daily Startup',
      key: 256
    }]
  },
  conditions: {
    selected: -99,
    options: [{
        name: 'Condition',
        value: -99
      },{
        name: 'more',
        value: 'more'
      },{
        name: 'equal',
        value: 'equal'
      },{
        name: 'less',
        value: 'less'
      }]
  }
}
```

Using `queryFormStatus()` function to get query result in json like:
```javascript
{
    "conditions": "and", 
    "rules": [
        {
            "keyid": "2", 
            "operater": "more", 
            "value": "1"
        }, 
        {
            "keyid": "2", 
            "operater": "equal", 
            "value": "3"
        }, 
        {
            "conditions": "or", 
            "rules": [
                {
                    "keyid": "1", 
                    "operater": "equal", 
                    "value": "4"
                }, 
                {
                    "keyid": "3", 
                    "operater": "equal", 
                    "value": "5"
                }, 
                {
                    "conditions": "and", 
                    "rules": [
                        {
                            "keyid": "2", 
                            "operater": "less", 
                            "value": "6"
                        }
                    ]
                }
            ]
        }
    ]
}
```