# detexify
A tool to recover origin tex code from the generated pdf file. 


## Step-by-step Realization of detexify
### Tex formula generater
A tex generater is a script used to generate training sets for neural network.  

### Segmentation of PDF file (hard code)
First, we need to segment the entire PDF file into lines. We call a line of pixels is empty if and only if the line of pixels containing no colored pixel. We define the largest set of continuous non-empty lines of pixels in a neighborhood of a non-empty line of pixels as a valid line. By recognizing each valid line, we complete the segmentation of a PDF file. 

### Recognize a valid line (CNN)
After segmenting the entire PDF file into valid lines, we recognize the objects by segmenting the lines with vertical empty lines. Each object will be classified by CNN and divided into several smaller objects recursively until we get all the objects be single characters.  

#### object: 
- table: a set of m times n objects (e.g. \binom, \bmatrix, \begin{cases}...\end{cases}, ...)
- fraction: a set of two objects 
- atom: a elementary unit of tex file which can not be divided vertically or horizontally
> object -> table | fraction | atom
> table -> object // object
> fraction -> \frac{object}{object}
> atom -> cmd{object} | object^object | object_object
> cmd -> \hat | \vec | \overline | \wtide | ...

### Encode the recognized elements into tex code 
