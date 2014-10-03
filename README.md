
# p97-angular-components

A collection of angular component used by Point 97.

Each components is contained in a directory strucuted as follows

##Installation

```

bower install p97-components

# Save to dependencies
bower install p97-components --save

```

This will install a directory named `p97-components` containing 
* p97-componnets.js
* p97-components.min.js
* question-types.js
* question-types.min.js
* templates/

```
<script src="PATH_TO_JS_LIB/p97-components/p97components.js"></script>
```

To update an existing installation use
```
bower install p97-angular-components --save
```


## For Developers

### Getting started
THIS SECTION IS INCOMPLETE
Clone repo and run 
```
npm install
```

### Creating Question Types

All directives must accept question and answer objects. Options for the question will be defined
in question.options.

All directives must record their answers in an answer object. Answer objects have the following
keywords

* value - A the actaull answer that is recorded. This could be a JSON object. 
* verbose (optional) - A human readable name to display as the answer.


## Example App
There is an example application used for testing and a tutorial located in `examples/`

This example is build on Yeoman and it's Angular generator. See http://yeoman.io/codelab/setup.html for more info. You will need Ruby installed and up-to-date, and node and npm installed and up-to-date.

To run the example app
cd example/
npm install
```
grunt serve
```

### Troubleshooting
If you get a compass error try 


```
sudo gem update --system
sudo gem install sass
sudo gem install compass
```





Viewpoint 2 defines ?? different question types. See the Viewppoint API at /api/v2/formstack/question-type/ to see the list. Each question type has a corresponding directive.

## Reference
### Question Types
Viewpoint 2 defines ?? different question types. See the Viewppoint API at /api/v2/formstack/question-type/ to see the list. Each question type has a corresponding directive.

* **datetime** 
 options
  * min 
  * max
  * required

* **number**
 options
  * min
  * max
  * required
 
* **textarea**
  `min_word` and `max_word` take precedence over `min_char` and `max_char`
 options
  * min_word
  * max_word
  * min_char
  * max_char
  * show_word_count
  * show_char_count

* **yes-no**
 options
 * default


### Making Question Type Components

####Directory structure
```
src/question-types/
 -- <directive-name>/
	 -- templates/
	 -- controllers.js
	 -- directives.js
```

#### Directive Scope
The scope takes three objects. 

```
        // Scope should always look like this in all question types.
        scope: {
            question: '=', 
            value: '=',
            control: '='
        },
```

 * **question** - This is a Viewpoint question object. Validation options are kept in `question.objects`
 
 * **value** - The actual raw value to record. This could be a string, a number, of a JSON object
 
 * **control** - The handle to attach function to you want exposed in the parent Controller.
 


### Question Methods
Each question type directive will have the following methods available. These are attached to the `control` object passed into the directive and are then available to the Controller.

```
// This is availible in the main controller.
scope.internalControl = scope.control || {};
scope.internalControl.validate_answer = function(){
	scope.errors = [];
	// Define your directive's validation here.
	
	// Add any error messages to errors array.
	
	return is_valid;  // A boolean	
}

scope.internalControl.clean_answer = function(){
	// Defined any data cleaning here e.g. time formats.
	// You should do this before validating. 
	// Acts on scope.value
};
```

* **clean_answer(answer)**
  Use this method to do any sort of pre-processing of data before passing it on to validate_answer(). For example hidden fields or computed fields that depend on related field's data. 

* **validate_answer(answer)**
  Returns: BOOLEAN
  This method takes the output of `clean_data()` and validates against the question options requirements. It returns the data is true, else it returns a list of validation errors to display on the UI. 
