# detexify
A tool to recover origin tex code from the generated pdf file. 


## Step-by-step Realization of detexify
### Tex formula generater


### Segmentation of PDF file (hard code)
First, we need to segment the entire PDF file into lines. We call a line of pixels is empty if and only if the line of pixels containing no colored pixel. We define the largest set of continuous non-empty lines of pixels in a neighbourhood of a non-empty line of pixels as a valid line. By recongnizing each valid line, we complete the segmentation of a PDF file. 

### Recongnize a valid line （
After segmenting the entire PDF file into valid lines, we recongnize the elements 


#### object: 

object -> table | fraction | atom
table -> object // object
fraction -> \frac{object}{object}
atom -> cmd{object} | object^object | object_object
cmd -> \hat | \vec | \overline | \wtide | ...

- table: a set of m times n objects (e.g. \binom, \bmatrix, \begin{cases}...\end{cases}, ...)
- fraction: a set of two objects 
- atom: a elementary unit of tex file which can not be divided v
