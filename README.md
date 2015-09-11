## LEARNING OBJECTIVES
Students will be able to…
- Explain what AJAX is and what benefits it offers for front end programming
- Identify the fundamental elements of an AJAX request
- Define JSON and Javascript Promises, and discuss their roles in asynchronous, object-oriented programming
- Use Vanilla Javascript to make an asynchronous ‘GET’ request for data


## LESSON PLAN

### OPENING FRAMING (2 min)

Up until this point, we’ve been dealing with HTTP requests entirely in the back end. Today we’re going to be looking at the basic structure of  AJAX which is a collection of techniques that allows us to send and receive server data on the client side (ie. in the browser).

#### What the heck is AJAX?!

> **A**synchronous
> **J**avascript
> **A**nd
> **X**ML

These are all words we’ve heard before. At a high level, who wants to take a stab at what that means?” Go word by word if necessary.

Basically, AJAX is a way of using technologies that we already know about and use in the front end to manage data exchange. Why? So we can update parts of a web page without having to do a full page refresh. AJAX is the basis of Single Page Applications, and the foundation for the front-end frameworks we’ll be looking at later in the course.


### WE DO (5 min)

#### T&T:
Take a look at this list of the fundamental building blocks of an AJAX request. Take a couple of minutes with the people around you to discuss how these might map onto an offline scenario. Maybe an errand? Maybe a fairy tale? Be creative....

1. Event occurs (browser side)
2. Create a request object (browser side)
3. Send the request object from browser to server
4. Process request object (server side)
5. Create a response object (server side)
6. Send response object back to the browser
7. Unpack the data from the response object and use it to update the page content (browser side)


### I DO (5 min)

#### Code Demo

There and two more new friends we need to get this party started. The first is...
  - **JSON**
    - JSON stands for JavaScript Object Notation
    - JSON is a lightweight data-interchange format
    - JSON is language independent (JSON uses JavaScript syntax, but the JSON format is text only, just like XML.
Text can be read and used as a data format by any programming language.)
    - JSON looks like this: Review!!!
    
> "But, I thought the "J" stood for Javascript! And where's the X?!"


### YOU DO (3 min)

[JSON Bourne](https://github.com/ebirving/JSON-bourne)







  - [**Promises**](http://www.html5rocks.com/en/tutorials/es6/promises/#toc-async)
    - "The promise constructor takes one argument, a callback with two parameters, resolve and reject. Do something within the callback, perhaps async, then call resolve if everything worked, otherwise call reject."
    - "'then' takes two arguments, a callback for a success case, and another for the failure case. Both are optional, so you can add a callback for the success or failure case only. 'then' isn't the end of the story, you can chain "then"s together to transform values or run additional async actions one after another."
  
```
function get(url) {
  // Return a new promise.
  return new Promise(function(resolve, reject) {
    // Do the usual XHR stuff
    var req = new XMLHttpRequest();
    req.open('GET', url);

    req.onload = function() {
      // This is called even on 404 etc
      // so check the status
      if (req.status == 200) {
        // Resolve the promise with the response text
        resolve(req.response);
      }
      else {
        // Otherwise reject with the status text
        // which will hopefully be a meaningful error
        reject(Error(req.statusText));
      }
    };

    // Handle network errors
    req.onerror = function() {
      reject(Error("Network Error"));
    };

    // Make the request
    req.send();
  });
}

get('story.json').then(JSON.parse).then(function(response) {
  console.log("Success!", response);
}, function(error) {
  console.error("Failed!", error);
});

```


