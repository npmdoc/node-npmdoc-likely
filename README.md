# api documentation for  [likely (v0.2.0)](https://github.com/sbyrnes/likely.js)  [![npm package](https://img.shields.io/npm/v/npmdoc-likely.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-likely) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-likely.svg)](https://travis-ci.org/npmdoc/node-npmdoc-likely)
#### Recommendation engine for Node.js applications.

[![NPM](https://nodei.co/npm/likely.png?downloads=true)](https://www.npmjs.com/package/likely)

[![apidoc](https://npmdoc.github.io/node-npmdoc-likely/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-likely_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-likely/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-likely/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-likely/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Sean Byrnes",
        "email": "sean@fogstack.com"
    },
    "bugs": {
        "url": "https://github.com/sbyrnes/likely.js/issues"
    },
    "dependencies": {
        "sylvester": ">=0.0.21"
    },
    "description": "Recommendation engine for Node.js applications.",
    "devDependencies": {
        "expresso": ">=0.9.2"
    },
    "directories": {},
    "dist": {
        "shasum": "6395fd3f7b065c813fdf49ad128658d278a9282c",
        "tarball": "https://registry.npmjs.org/likely/-/likely-0.2.0.tgz"
    },
    "engines": {
        "node": ">=0.6.13"
    },
    "gitHead": "aa49560d97eac6114d362733b479debc0468eefd",
    "homepage": "https://github.com/sbyrnes/likely.js",
    "keywords": [
        "recommendation",
        "learning",
        "matrix"
    ],
    "main": "./likely.js",
    "maintainers": [
        {
            "name": "sbyrnes",
            "email": "sean@fogstack.com"
        }
    ],
    "name": "likely",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/sbyrnes/likely.js.git"
    },
    "scripts": {},
    "version": "0.2.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module likely](#apidoc.module.likely)
1.  [function <span class="apidocSignatureSpan">likely.</span>Bias (average, rowBiases, colBiases)](#apidoc.element.likely.Bias)
1.  [function <span class="apidocSignatureSpan">likely.</span>Model (inputMatrix, rowLabels, colLabels)](#apidoc.element.likely.Model)
1.  [function <span class="apidocSignatureSpan">likely.</span>buildModel (inputArray, rowLabels, colLabels)](#apidoc.element.likely.buildModel)
1.  [function <span class="apidocSignatureSpan">likely.</span>buildModelWithBias (inputArray, bias, rowLabels, colLabels)](#apidoc.element.likely.buildModelWithBias)
1.  [function <span class="apidocSignatureSpan">likely.</span>calculateBias (input)](#apidoc.element.likely.calculateBias)
1.  [function <span class="apidocSignatureSpan">likely.</span>calculateColumnAverage (inputMatrix)](#apidoc.element.likely.calculateColumnAverage)
1.  [function <span class="apidocSignatureSpan">likely.</span>calculateError (estimated, input, bias)](#apidoc.element.likely.calculateError)
1.  [function <span class="apidocSignatureSpan">likely.</span>calculateMatrixAverage (inputMatrix)](#apidoc.element.likely.calculateMatrixAverage)
1.  [function <span class="apidocSignatureSpan">likely.</span>calculateRowAverage (inputMatrix)](#apidoc.element.likely.calculateRowAverage)
1.  [function <span class="apidocSignatureSpan">likely.</span>calculateTotalError (errorMatrix)](#apidoc.element.likely.calculateTotalError)
1.  [function <span class="apidocSignatureSpan">likely.</span>generateRandomMatrix (rows, columns)](#apidoc.element.likely.generateRandomMatrix)
1.  number <span class="apidocSignatureSpan">likely.</span>ALPHA
1.  number <span class="apidocSignatureSpan">likely.</span>BETA
1.  number <span class="apidocSignatureSpan">likely.</span>DESCENT_STEPS
1.  number <span class="apidocSignatureSpan">likely.</span>K
1.  number <span class="apidocSignatureSpan">likely.</span>MAX_ERROR
1.  object <span class="apidocSignatureSpan">likely.</span>Model.prototype

#### [module likely.Model](#apidoc.module.likely.Model)
1.  [function <span class="apidocSignatureSpan">likely.</span>Model (inputMatrix, rowLabels, colLabels)](#apidoc.element.likely.Model.Model)

#### [module likely.Model.prototype](#apidoc.module.likely.Model.prototype)
1.  [function <span class="apidocSignatureSpan">likely.Model.prototype.</span>rankAllItems (row)](#apidoc.element.likely.Model.prototype.rankAllItems)
1.  [function <span class="apidocSignatureSpan">likely.Model.prototype.</span>recommendations (row)](#apidoc.element.likely.Model.prototype.recommendations)



# <a name="apidoc.module.likely"></a>[module likely](#apidoc.module.likely)

#### <a name="apidoc.element.likely.Bias"></a>[function <span class="apidocSignatureSpan">likely.</span>Bias (average, rowBiases, colBiases)](#apidoc.element.likely.Bias)
- description and source-code
```javascript
function Bias(average, rowBiases, colBiases) {
	this.average = average;		// Overall value average
	this.rowBiases = rowBiases; // Bias for each row
	this.colBiases = colBiases;	// Bias for each column
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.likely.Model"></a>[function <span class="apidocSignatureSpan">likely.</span>Model (inputMatrix, rowLabels, colLabels)](#apidoc.element.likely.Model)
- description and source-code
```javascript
function Model(inputMatrix, rowLabels, colLabels) {
	this.rowLabels = rowLabels;	// labels for the rows
	this.colLabels = colLabels; // labels for the columns
	this.input = inputMatrix;	// input data
	
	// estimated data, initialized to all zeros
	this.estimated = sylvester.Matrix.Zeros(this.input.rows(),this.input.cols());
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.likely.buildModel"></a>[function <span class="apidocSignatureSpan">likely.</span>buildModel (inputArray, rowLabels, colLabels)](#apidoc.element.likely.buildModel)
- description and source-code
```javascript
function buildModel(inputArray, rowLabels, colLabels)
{
	return buildModelWithBias(inputArray, undefined, rowLabels, colLabels);
}
```
- example usage
```shell
...
    var colLabels = ['Red', 'Blue', 'Green', 'Purple'];

Using these values, John rates Red 1 while Joe rates Red 7. Sue has no rating for Blue.

#### STEP 2. Train the model
Using the inputMatrix you build a model, which estimates the ratings for all entities for all users.
<!-- language: lang-js -->
    var Model = Recommender.buildModel(inputMatrix, rowLabels, colLabels);

or, if you don't have or care about labels
<!-- language: lang-js -->
    var Model = Recommender.buildModel(inputMatrix);

The Model object now contains a matrix of the same size as inputMatrix but with estimates ratings for
all items for all entities.
...
```

#### <a name="apidoc.element.likely.buildModelWithBias"></a>[function <span class="apidocSignatureSpan">likely.</span>buildModelWithBias (inputArray, bias, rowLabels, colLabels)](#apidoc.element.likely.buildModelWithBias)
- description and source-code
```javascript
function buildModelWithBias(inputArray, bias, rowLabels, colLabels)
{
	var model = new Model($M(inputArray), rowLabels, colLabels);
	model.estimated = train(sylvester.Matrix.create(inputArray), bias);
	
	return model
}
```
- example usage
```shell
...
In a lot of input data there is inherent bias. For example, a given user might tend to rate a great movie as 10 stars which another
 user never gives above 8 stars.
These inherent biases can skew the estimations by providing false signals to the model. To handle these, you can adjust for biases
 by including them in your model
building.
<!-- language: lang-js -->	
	var bias = Recommender.calculateBias(input);
	
    // Build the model using the training set and considering the bias
    var model = Recommender.buildModelWithBias(trainingSet, bias);
	
The resulting model should be very similar to the one obtained without providing bias, but more accurate.

FAQ
---------
#### I used Likely.js to generate recommendations based on my data. How do I know if it's working?
...
```

#### <a name="apidoc.element.likely.calculateBias"></a>[function <span class="apidocSignatureSpan">likely.</span>calculateBias (input)](#apidoc.element.likely.calculateBias)
- description and source-code
```javascript
function calculateBias(input)
{
	var inputMatrix = $M(input);
	var average = calculateMatrixAverage(inputMatrix);
	var rowAverages = calculateRowAverage(inputMatrix);
	var colAverages = calculateColumnAverage(inputMatrix);
	
	var rowBiases = new Array();
	var colBiases = new Array();
	
	// The row bias is the difference between the row average and the overall average
	for(var i = 1; i <= rowAverages.dimensions().cols; i++)
	{
		rowBiases[i-1] = rowAverages.e(i) - average;
	}
	
	// the column bias is the difference between the column average and the overall average
	for(var i = 1; i <= colAverages.dimensions().cols; i++)
	{
		colBiases[i-1] = colAverages.e(i) - average;
	}
	
	var biases = new Bias(average, $V(rowBiases), $V(colBiases));
	
	return biases;
}
```
- example usage
```shell
...

Handling Bias
---------
In a lot of input data there is inherent bias. For example, a given user might tend to rate a great movie as 10 stars which another
 user never gives above 8 stars.
These inherent biases can skew the estimations by providing false signals to the model. To handle these, you can adjust for biases
 by including them in your model
building.
<!-- language: lang-js -->	
	var bias = Recommender.calculateBias(input);
	
    // Build the model using the training set and considering the bias
    var model = Recommender.buildModelWithBias(trainingSet, bias);
	
The resulting model should be very similar to the one obtained without providing bias, but more accurate.

FAQ
...
```

#### <a name="apidoc.element.likely.calculateColumnAverage"></a>[function <span class="apidocSignatureSpan">likely.</span>calculateColumnAverage (inputMatrix)](#apidoc.element.likely.calculateColumnAverage)
- description and source-code
```javascript
function calculateColumnAverage(inputMatrix)
{
	var rows = inputMatrix.rows();
	
	var averages = new Array();
	for(var i = 1; i <= inputMatrix.cols(); i++)
	{
		var sum = 0;
		for(var j = 1; j <= inputMatrix.rows(); j++)
		{
			sum += inputMatrix.e(j, i);
		}
		averages[i-1] = sum/rows;
	}
	
	return $V(averages);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.likely.calculateError"></a>[function <span class="apidocSignatureSpan">likely.</span>calculateError (estimated, input, bias)](#apidoc.element.likely.calculateError)
- description and source-code
```javascript
function calculateError(estimated, input, bias)
{ 	
	var adjustedInput = input.dup();
	
	var adjustedElements = adjustedInput.elements;
		
	// If bias adjustment is provided, adjust for it
	if(bias)
	{
		// subtract the row and column bias from each row
		for(var i = 0; i <= adjustedInput.rows()-1; i++)
		{
			for(var j = 0; j <= adjustedInput.cols()-1; j++)
			{
				if(adjustedElements[i][j] == 0) continue; // skip zeroes
				
				adjustedElements[i][j] -= bias.average;
				
				adjustedElements[i][j] -= bias.rowBiases.e(i+1);
				
				adjustedElements[i][j] -= bias.colBiases.e(j+1);
			}
		}
	}
	
	
	var estimatedElements = estimated.elements;
	
	// Error is (R - R')
	// (but we ignore error on the zero entries since they are unknown)
	for(var i = 0; i <= adjustedInput.rows()-1; i++)
	{
		for(var j = 0; j <= adjustedInput.cols()-1; j++)
		{
			if(adjustedElements[i][j] == 0) continue; // skip zeroes
			
			adjustedElements[i][j] -= estimatedElements[i][j];
		}
	}				

	// Error is (R - R')
	return adjustedInput;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.likely.calculateMatrixAverage"></a>[function <span class="apidocSignatureSpan">likely.</span>calculateMatrixAverage (inputMatrix)](#apidoc.element.likely.calculateMatrixAverage)
- description and source-code
```javascript
function calculateMatrixAverage(inputMatrix)
{
	var cells = inputMatrix.rows() * inputMatrix.cols();
	
	var sum = 0;
	for(var i = 1; i <= inputMatrix.rows(); i++)
	{
		for(var j = 1; j <= inputMatrix.cols(); j++)
		{
			sum += inputMatrix.e(i, j);
		}
	}
	
	return sum/cells;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.likely.calculateRowAverage"></a>[function <span class="apidocSignatureSpan">likely.</span>calculateRowAverage (inputMatrix)](#apidoc.element.likely.calculateRowAverage)
- description and source-code
```javascript
function calculateRowAverage(inputMatrix)
{
	var cols = inputMatrix.cols();
	
	var averages = new Array();
	for(var i = 1; i <= inputMatrix.rows(); i++)
	{
		var sum = 0;
		for(var j = 1; j <= inputMatrix.cols(); j++)
		{
			sum += inputMatrix.e(i, j);
		}
		averages[i-1] = sum/cols;
	}
	
	return $V(averages);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.likely.calculateTotalError"></a>[function <span class="apidocSignatureSpan">likely.</span>calculateTotalError (errorMatrix)](#apidoc.element.likely.calculateTotalError)
- description and source-code
```javascript
function calculateTotalError(errorMatrix)
{
	var totError = 0.0;
	for(var i = 1; i <= errorMatrix.rows(); i++)
	{
		for(var j = 1; j <= errorMatrix.cols(); j++)
		{
			totError += Math.pow(errorMatrix.e(i, j), 2);
		}
	}
	
	return totError;
}
```
- example usage
```shell
...
<!-- language: lang-js -->
    var Recommender = require('likely.js');

    // Build the model using the training set
    var model = Recommender.buildModel(trainingSet);
	
    // Calculate the error from the produced model against the CV set of known values
    var totalError = Recommender.calculateTotalError(model.estimate, crossValidationSet);


#### I trained a model using my training set but the error is too high against my CV set. What do I do?

This is common for any machine learning application. In this case it will be necessary to tune the parameters of the
Likely.js learning algorithm to better fit your data. The available options that you can adjust are as follows:
<!-- language: lang-js -->
...
```

#### <a name="apidoc.element.likely.generateRandomMatrix"></a>[function <span class="apidocSignatureSpan">likely.</span>generateRandomMatrix (rows, columns)](#apidoc.element.likely.generateRandomMatrix)
- description and source-code
```javascript
function generateRandomMatrix(rows, columns)
{
	return sylvester.Matrix.Random(rows, columns);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.likely.Model"></a>[module likely.Model](#apidoc.module.likely.Model)

#### <a name="apidoc.element.likely.Model.Model"></a>[function <span class="apidocSignatureSpan">likely.</span>Model (inputMatrix, rowLabels, colLabels)](#apidoc.element.likely.Model.Model)
- description and source-code
```javascript
function Model(inputMatrix, rowLabels, colLabels) {
	this.rowLabels = rowLabels;	// labels for the rows
	this.colLabels = colLabels; // labels for the columns
	this.input = inputMatrix;	// input data
	
	// estimated data, initialized to all zeros
	this.estimated = sylvester.Matrix.Zeros(this.input.rows(),this.input.cols());
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.likely.Model.prototype"></a>[module likely.Model.prototype](#apidoc.module.likely.Model.prototype)

#### <a name="apidoc.element.likely.Model.prototype.rankAllItems"></a>[function <span class="apidocSignatureSpan">likely.Model.prototype.</span>rankAllItems (row)](#apidoc.element.likely.Model.prototype.rankAllItems)
- description and source-code
```javascript
rankAllItems = function (row)
	{
		var rowIndex = row; // assume row is a number
		// If we're using labels we have to look up the row index
		if(this.rowLabels)
		{
			rowIndex = findInArray(this.rowLabels, row);
		}
		
		// estimates for this user
		var ratingElements = this.estimated.row(rowIndex+1).elements;
		
		// build a two dimensional array from the ratings and indexes
		//     [[index, rating], [index, rating]]
		var outputArray = new Array();
		for(var i=0; i<ratingElements.length; i++)
		{
			outputArray[i] = [i, ratingElements[i]];
			
			// if we have column labels, use those
			if(this.colLabels)
			{
				outputArray[i][0] = this.colLabels[i];
			}
		}
		
		// Sort the array by index
		return outputArray.sort(function(a, b) {return a[1] < b[1]})
	}
```
- example usage
```shell
...
<!-- language: lang-js -->
var recommendations = model.recommendations(0);
	
// recommendations = [[3, 1.34]];

**Example 3**: Retrieve a list of all items, sorted by the ratings for a given user (both estimated and actual), using labels.
<!-- language: lang-js -->
var allItems = model.rankAllItems('John');
	
// allItems = [['Green', 3.00], ['Blue', 2.00], ['Purple', 1.34], ['Red', 1.00]];

**Example 4**: Retrieve a list of all items, sorted by the ratings for a given user (both estimated and actual) without labels.
<!-- language: lang-js -->	
var allItems = model.rankAllItems(0);
...
```

#### <a name="apidoc.element.likely.Model.prototype.recommendations"></a>[function <span class="apidocSignatureSpan">likely.Model.prototype.</span>recommendations (row)](#apidoc.element.likely.Model.prototype.recommendations)
- description and source-code
```javascript
recommendations = function (row)
	{
		var recommendedItems = new Array();
		var allItems = this.rankAllItems(row);
			
		var rowIndex = row; // assume row is a number
		// If we're using labels we have to look up the row index
		if(this.rowLabels)
		{
			rowIndex = findInArray(this.rowLabels, row);
		}
		
		for(var i=0; i< allItems.length; i++)
		{
			// look up the value in the input
			var colIndex = allItems[i][0];
			// see if we're using column labels or not
			if(this.colLabels)
			{
				colIndex = findInArray(this.colLabels, allItems[i][0]);
			}
			
			var inputRating = this.input.e(rowIndex+1, colIndex+1);
			
			// if there was no rating its a recommendation so add it
			if(inputRating == 0)
			{
				recommendedItems.push(allItems[i]);
			}
		}
		
		return recommendedItems;
	}
```
- example usage
```shell
...
all items for all entities.

#### STEP 3. Extract recommendations
There are a few ways to retrieve recommendations from the model you have built.

**Example 1**: Retrieve a list of all items not already rated by a user, sorted by estimated ratings using labels.
<!-- language: lang-js -->
var recommendations = model.recommendations('John');
	
// recommendations = [['Purple', 1.34]];


**Example 2**: Retrieve a list of all items not already rated by a user, sorted by estimated ratings without labels.
<!-- language: lang-js -->
var recommendations = model.recommendations(0);
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
