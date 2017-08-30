# prospectimo

Get the temporal orientation (time perspective) of a string.

## Usage
```javascript
const prospectimo = require('prospectimo');
const opts = {
  'encoding': 'binary',
  'max': Number.POSITIVE_INFINITY,
  'min': Number.NEGATIVE_INFINITY,
  'nGrams': 'true',
  'output': 'orientation',
  'places': 9,
  'sortBy': 'freq',
  'wcGrams': 'false',
};
const str = 'A big long string of text...';
const orientation = prospectimo(str, opts);
console.log(orientation);
```

## The Options Object

The options object is optional and provides a number of controls to allow you to tailor the output to your needs. However, for general use it is recommended that all options are left to their defaults.

### 'encoding'

**String - valid options: 'freq' (default), 'binary'**

N.B - You probably don't want to change this, ever.

Controls how the lexical value is calculated.

Binary is simply the addition of lexical weights, i.e. word1 + word2 + word3.

Frequency encoding takes the overall wordcount and word frequency into account, i.e. (word frequency / word count) * weight.

### 'output'

**String - valid options: 'orientation' (default), 'matches', 'lex', or 'full'**

'orientation' (default) returns the predicted temporal orientation as a string, i.e. "Past", "Present", "Future", or "Unknown".

'lex' returns an object with the lexical value for past, present and future orientations.

'matches' returns an array of matched words along with the number of times each word appears, its weight, and its final lexical value. See the output example below for an example.

'full' returns an object containing the lexical value and the matches array.

### 'nGrams'

**String - valid options: 'true' (default) or 'false'**

n-Grams are contiguous pieces of text, bi-grams being chunks of 2, tri-grams being chunks of 3, etc.

Use the nGrams option to include (true) or exclude (false) n-grams. For accuracy it is recommended that n-grams are included, however including n-grams for very long strings can detrement performance.

### 'wcGrams'

**String - valid options: 'true' or 'false' (default)**

When set to true, the output from the nGrams option will be added to the word count.

For accuracy it is recommended that this is set to false.

### 'sortBy'

**String - valid options: 'freq' (default)', 'weight', or 'lex'**

If 'output' = 'matches', this option can be used to control how the outputted array is sorted.

'lex' sorts by final lexical value, i.e. (word frequency * word count) / word weight.

'weight' sorts the array by the matched words initial weight.

'freq' (default) sorts by word frequency, i.e. the most used words appear first.

### 'places'

**Number**

Number of decimal places to limit outputted values to.

The default is 9 decimal places.

### 'max' and 'min'

**Float**

Exclude words that have weights above the max threshold or below the min threshold.

By default these are set to infinity, ensuring that no words from the lexicon are excluded.

The smallest value in the lexicon is -0.9772179. Therefore a threshold of -0.98 will include all words in the lexicon.

The largest value in the lexicon is 1.15807005. Therefore a threshold of 1.16 will include no words in the lexicon.

## Acknowledgements

### References
[Schwartz, H. A., Park, G., Sap, M., Weingarten, E., Eichstaedt, J., Kern, M., Stillwell, D., Kosinski, M., Berger, J., Seligman, M., & Ungar, L. (2015). Extracting Human Temporal Orientation from Facebook Language. NAACL-2015: Conference of the North American Chapter of the Association for Computational Linguistics.](http://www.seas.upenn.edu/~hansens/tempor-naacl15-cr.pdf).

[Park, G., Schwartz, H.A., Sap, M., Kern, M.L., Weingarten, E., Eichstaedt, J.C., Berger, J., Stillwell, D.J., Kosinski, M., Ungar, L.H. & Seligman, M.E. (2015). Living in the Past, Present, and Future: Measuring Temporal Orientation with Language. Journal of personality.](http://wwbp.org/papers/Park_et_al-2016-Journal_of_Personality.pdf).

### Lexicon
Using the prospection lexicon data from [WWBP](http://www.wwbp.org/lexica.html) under the [Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported](http://creativecommons.org/licenses/by-nc-sa/3.0/).

## Licence
(C) 2017 [P. Hughes](https://www.phugh.es).

[Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported](http://creativecommons.org/licenses/by-nc-sa/3.0/).