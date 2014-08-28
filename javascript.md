# JavaScript guide

## Style

0. Recommend to follow this style https://github.com/stephenplusplus/javascript-style
1. Chained methods should be split into multiple lines

  ```js
  // Not preferred
  surveys.sync()
    .filter(function (survey) {
      return record.expired;
    })
    .map(function (survey) {
      survey.records = survey.data.length;
      return survey;
    })
    .save();
  ```
  
  ```js
  // Preferred 
  function expired (survey) {
    return record.expired;
  }
  
  function counts (survey) {
    survey.records = survey.data.length;
    return survey;
  }
  
  surveys.sync()
    .filter(expired)
    .map(counts)
    .save();
  ```
2. Multiple var statements 
3. if else

  ```js
  if (err) {
    return res.json(400, { errors: ['There are no incidents']  });
  }
  
  // if you have a large expression to evaluate, write a method
  
  function executable () {
    return !survey.changed && 
      (!survey.expired || survey.expires === 'never');
  }
  
  if (survey.changed) {
    // do something
  } else if (executable()) {
    // do this
  } else {
    // do something else
  }
  ```
4. Ternary operators

  ```js
  var exp = this.val1 < this.val2
    ? 'good'
    : 'bad';
  ```
5. Spacing and other preferred practices 

  ```js
  // Good
  if (err)  
  // Bad
  if(err)   
  
  // Good
  function () {}  
  // Bad
  function(){}    
  
  // Good
  var sum = val1 + val2     
  // Bad
  var sum = val1+val2       
  
  // Bad
  var path = '/organizations/' + organization._id + '/surveys/' + survey._id 
  // Good
  var path = [
    '/organizations',
    organization._id,
    'surveys',
    survey._id
  ].join('/');
  
  // Good
  function expired () {
    return survey.expires < new Date();
  }
  // Bad
  function expired () {
    return survey.expires < new Date();
    ? true
    : false;
  }
  ```
6. Precendence for requiring

  ```js
  var http = require('http');                       // native modules first
  var mongoose = require('mongoose');               // npm modules second
  var config = require('config');                   // modules that are required via NODE_PATH third
  var fmt = require('./format-date');               // local modules fourth
  var oauthHelper = require('../../oauth-helper');  // relative modules last
  ```
7. `snake_case` for naming database attributes
8. `camelCase` for variables and methods. 
9. `Constructors` start with caps.
10. `file-names` and `folder-names` must use hyphens and not underscores or caps.
  
## Further reading 

1. [function qualityGuide](https://github.com/bevacqua/js)
