# SancaML
A prototype for a new markup language for complex interactive documents that publish both for PDF and HTML

## Stages

  1. Run the macro preprocessor.
  2. Convert the markdown commands to XML tags.
  3. Convert the resulting XML into HTML 5 and PDF.

## The Macro Preprocessor

```
# Comments begin with a number/hash sign.
# Nice Unicode support
Hello world! @+266B@(Beamed Eighth Notes)♫

# Escaping
@@

# Simple macros. @: defines new macros, @1 is the first argument
@:Hello(1){Hello @1.}

# Invocation is simple:
@Hello(macros)

# We can overload macros
@:Hello(){Hello World again!}
@Hello()
```

Outpus:

```
Hello world! ♫♫♫

@

Hello macros!
Hello World again!
```

## Markdown on XML

```
<p>This is a paragraph with an emoji (:ice_cream:) on a link: [<emoji name="ice_cream"/>](https://emojipedia.org/ice-cream/)</p>
```

This is paragraph has an emoji (🍨) on a link: [🍨](https://emojipedia.org/ice-cream/)

## Some tags

| Tag           | Meaning       |
| ------------- | ------------- |
| ```<abr>```   | Abreviation (the screen reader will read the full text)  |
| ```<acr>```   | Acronymum  |
| ```<pr>```    | Pronunciation |
| ```<p>```     | Paragraph |
| ```<l>```     | Link |
| ```<c>```     | Citation |
| ```<bib>```   | Bibliographical work |


```
<abr for="Rest in Peace">RIP</abr>
<acr for="HyperText Markup Language">RIP</acr>
<pr as="closure">Clojure</pr>
<pr as="[ʒeˈtulju doɾˈnɛlis ˈvaɾɡɐs]">Getúlio Dornelles Vargas</pr>
<c work="boring book"/> # Outputs things like: [1]; [Smith, J et al. 1837];
<bib institution="monsters-u" acr="MU">Monsters University</bib>
<bib work="boring book">
  <title>On Scary Theory</title>
  <author email="jsmith@example.com" affiliation="monsters-u">John Smith</author>
  <author>Forgotten guy</author>
  <date>01-Oct-1837</date> # Or: 1837-10-01
  <url>example.com/jsmith/1837/scary.pdf</url>
</bib>
```
