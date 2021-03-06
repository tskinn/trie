# trie
A trie data structure created for the sole purpose of easily reducing a large list of strings into a small list of strings.

More specifically, this library was created with only one use case in mind. A certain CDN only allows a small 
number of concurrent purge requests. If you have a thousands of purgeable files with frequent purges of various
combinations of these files things get a little more complicated. You don't want to purge the contents of the entire
folder every time you need to purge something but you also don't want to wait a long time for files to be purged. Fortunately, 
the CDN supports file globbering or the use of the '*' as a wildcard at the end of filename. So it is possible to purge these files:

```Bash
somefile.txt
someotherfile.txt
some.txt
```

with thise purge request:

```Bash
some*
```

This library makes it easy to generate a handful of purge strings from large lists of resources to be purged. Try it out by
running the test file or experimenting on the list of files given in `testset.txt` in this repo.


## Example

``` text
test
testify
testament
testimony
tesseract
tess
```

If one were to insert every string from the list above into a `trie` a
structure that resembles the following diagram would be made.


``` text
          ['t']
            |
         ['es']
        /      \
    ['s']      ['t']
     /         /    \
['eract'] ['ament']  ['i']
                     /   \
                 ['fy']  ['mony']
``` 

Then if you were to DeleteWords(6, '*') then you would end up with something like this:

``` text
          ['t']
            |                      test
         ['es']                    tess
        /      \                   testament
    ['s']      ['t']               tesseract
     /         /    \              testi*
['eract'] ['ament']  ['i*']
``` 

Or if you wer to run DeleteWords(3, '*') you would get something like this:

``` text
          ['t']                    tess*
            |                      test*
         ['es']
        /      \
    ['s*']      ['t*']
``` 
