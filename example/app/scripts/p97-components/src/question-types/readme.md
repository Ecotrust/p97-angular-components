# Question Types

Viewpoint 2 defines ?? different question types. See the Viewppoint API at /api/v2/formstack/question-type/ to see the list. Each question type has a corresponding directive.

## Question Types

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



## Question Type Directives
The scope takes three objects. 

 * question - This is a Viewpoint question object. Validation options are kept in `question.objects`
 
 * value - The actual raw value to record. This could be a string, a number, of a JSON object
 
 * control - The handle to attach function to you want exposed in the parent Controller.
 
```
scope: {
            question: '=', 
            value: '=',
            control: '='
        },
```

### Question Methods
Each question type directive will have the following methods available. These are attached to the `control` object passed into the directive and are then available to the Controller.


* **clean_answer(answer)**
  Use this method to do any sort of pre-processing of data before passing it on to validate_answer(). For example hidden fields or computed fields that depend on related field's data. 

* **validate_answer(answer)**
  Returns: BOOLEAN
  This method takes the output of `clean_data()` and validates against the question options requirements. It returns the data is true, else it returns a list of validation errors to display on the UI. 