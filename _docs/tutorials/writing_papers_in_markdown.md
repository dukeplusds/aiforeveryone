---
title: Writing Papers in Markdown
category: Tutorials
order: 12
---

I have asked that in addition to your final project report in PDF format, you also submit a report to be displayed on this site in markdown.

Markdown is an easy-to-use format to render text on a webpage without using HTML. This entire site is written in Markdown.
Markdown files end in the `.md` format rather than .doc or .pdf.  Converting your file from a Word document to a Markdown document should be as simple as copy and paste with a few minor changes. Please find a guide to using markdown for your reports below:

### Text

Make some words **bold** and other words *italic* with Markdown. Make a [link](http://google.com)

```md
Make some words **bold** and other words *italic* with Markdown. Make a [link](http://google.com)
```


### Equations

Equations should be written like LaTex but start and end with `$$`

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

```md
$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$
```

### Lists

Numbered lists:

1. One
2. Two
3. Three

Bullet points:

* this is my first point
* this is my second point

Dashes,

- Some dashes
- Some sub-points:
  - Like this
  - And this

```md
Numbered lists:

1. One
2. Two
3. Three

Bullet points:

* this is my first point
* this is my second point

Dashes,

- Some dashes
- Some sub-points:
  - Like this
  - And this
```

### Images
If you want to embed images, this is how you do it:

![my graph](https://i.pinimg.com/originals/10/54/e8/1054e8b90d3b4637688cc904e6a7c915.png)

```md
![my graph](https://i.pinimg.com/originals/10/54/e8/1054e8b90d3b4637688cc904e6a7c915.png)
```

If you have images that you'd like to include, they can also come from a local folder. I'll reformat them:

<img src="{{ "/images/tutorials/output_22_1.png" | prepend: site.baseurl }}{{ img }}" alt="">

```md
![my local graph](images/tutorials/output_22_1.png)
```




### Document Structure
Headings to structure your documents. Start lines with a `#` to create headings. Multiple `##` in a row denote smaller heading sizes.

# Make a Heading

#### A smaller heading

```md
# Make a Heading

#### A smaller heading
```



### Add a quote like so

> This is a brilliant quote
> - Matthew Kenney

```
> This is a brilliant quote
> - Matthew Kenney
```

### Code
You can also include code snippets. They should be wrapped in the triple dash symbol. To add syntax highlighting you can say [triple dash]python:

```python
def hello_word(x, y):
    output = x + y
    return output
```


### Lists

- [x] This is a complete item
- [ ] This is an incomplete item

```md
- [x] This is a complete item
- [ ] This is an incomplete item
```

