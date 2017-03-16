# week4-ammp

The spectacular ammp autocompletion engine



## Performance of generating an array using `filter`, `match`, `exec`

```javascript
// Option 1: filter
const wordsArr = file.slice(0, -1).split('\n');
const matchingWordArr = wordsArr.filter(word => {
  const pattern = new RegExp(searchQuerySanitized, 'i');
  return pattern.test(word);
});
// Time to get results: 200 ms

// Option 2: match
const pattern = new RegExp(`\\b.*${searchQuerySanitized}.*\\b`, 'gi');
const matchingWordArr = file.match(pattern) || [];
// Time to get results: 50 ms

// Option 3: exec
function getMatchingWordArr(searchQuerySanitized, file) {
  const pattern = new RegExp(`\\b.*${searchQuerySanitized}.*\\b`, 'gi');

  const matchingWordArr = [];

  let match;
  let numberOfMatches = 0;

  while ((match = pattern.exec(file)) !== null && numberOfMatches < 100) {
    matchingWordArr.push(match[0]);
    numberOfMatches++;
  }

  return matchingWordArr;
}
// Time to get results: 10 ms
```

## Sanitizing the input text

 ```javascript
 // Extract the search query from the request url
 const searchQuery = url.parse(request.url, true).query.search;

 // Remove all non-letters
 const searchQuerySanitized = searchQuery.replace(/[^a-z]/gi, '');
 ```
