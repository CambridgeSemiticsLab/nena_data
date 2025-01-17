# Nena Markup Format

NENA texts are transcribed stories or dialogues derived from audio recordings in 
the field. These transcriptions have traditionally taken the form of publications 
or files stored on a personal computer. In the NENA text-corpus project we normalize 
these various formats into a simple plain-text version. This version is intended 
to be both human- and machine-readable and include annotations. Markup languages 
like [Markdown](https://daringfireball.net/projects/markdown/syntax) are examples
of hybrid formats which are easy for people to use and can be read by machines 
with some basic parsing. 

The NENA Markup Format is a simple plain-text format for inputting and annotating
NENA transcriptions. The format outlined below is inspired both by Markdown and, 
more distantly, by the Eep Talstra Centre for Bible and Computer's 
[PIL text format](https://github.com/ETCBC/data_creation/blob/master/documentation/pil_format.pdf)
used for Aramaic and Hebrew corpora.

**Contents**

* [Example of NENA Markup](#Example-of-NENA-Markup-Text)
* [Structure](#Structure)
  * [Metadata Block](#Metadata-block)
  * [Text Block](#text-block)
    * [Canonical Letters](#Canonical-letters)
    * [Foreign Letters](#Foreign-letters)
    * [Paragraph Structure](#Paragraph-structure)
    * [Punctuation](#Punctuation)
    * [Span Tag](#Span-Tag)
    * [Foreign Language Tag](#Foreign-Language-Tag)

## Example of NENA Markup Text

Below is an example of a text annotated with NENA Markup. The markup is mainly 
hypothetical for illustrative purposes and contains all possible markup patterns.

```
dialect = Urmi_C
title = When Shall I Die?
encoding = UTF8
informant = Yulia Davudi
interviewer = Geoffrey Khan
place = +Hassar +Baba-čanɟa, N
transcriber = Geoffrey Khan
text_id = A32 

(1@0:00) xá-yuma ⁺malla ⁺Nasrádən váyələ tíva ⁺ʾal-k̭èsa.ˈ xá mən-nášə 
⁺vàrəva,ˈ mə́rrə ⁺màllaˈ ʾátən ʾo-k̭ésa pràmut,ˈ bət-nàplət.ˈ mə́rrə <P:bŏ́ro> 
bàbaˈ ʾàtən=daˈ ⁺šúla lə̀tluxˈ tíyyət b-dìyyi k̭ítət.ˈ ⁺šúk̭ si-⁺bar-⁺šùlux.ˈ 
ʾána ⁺šūl-ɟànilə.ˈ náplən nàplən.ˈ (2@0:08) ⁺hàlaˈ ʾo-náša léva xíša xá 
⁺ʾəsrá ⁺pasulyày,ˈ ⁺málla bitáyələ drúm ⁺ʾal-⁺ʾàrra.ˈ bək̭yámələ ⁺bərxáṱələ 
⁺bàru.ˈ màraˈ ⁺maxlèta,ˈ ʾátən ⁺dílux ʾána bət-náplənva m-⁺al-ʾilàna.ˈ 
bas-tánili xázən ʾána ʾíman bət-mètən.ˈ ʾo-náša xzílə k̭at-ʾá ⁺màllaˈ hónu 
xáč̭č̭a ... ⁺basùrələˈ mə́rrə k̭àtuˈ ⁺maxlèta,ˈ mə̀drə,ˈ «GK:maxlèta?» ⁺rába 
⁺maxlèta.ˈ mə́rrə k̭at-ʾíman xmártux ⁺ṱlá ɟáhə ⁺ʾarṱàla,ˈ ʾó-yuma mètət.ˈ 
ʾó-yumət xmártux ⁺ṱlá ɟáhə ⁺ʾarṱàla,ˈ ʾó-yuma mètət.ˈ 

(3@0:16) ⁺málla múttəva ... ⁺ṱànaˈ ⁺yak̭úyra ⁺ʾal-xmàrta.ˈ ⁺ṱànaˈ mə́ndi 
⁺rába múttəva ⁺ʾal-xmàrtaˈ ʾu-xmàrtaˈ ⁺báyyava ʾask̭áva ⁺ʾùllul.ˈ
ʾu-bas-pòxa ⁺plə́ṱlə mənnó.ˈ ṱə̀r,ˈ ⁺riṱàla.ˈ ⁺málla mə́rrə ʾàha,ˈ ʾána dū́n
k̭arbúnə k̭a-myàta.ˈ (4@0:20) xáč̭č̭a=da sə̀k̭laˈ xa-xìta.ˈ ɟánu mudməxxálə
⁺ʾal-⁺ʾàrra.ˈ mə̀rrəˈ xína ⁺dā́n mòtila.ˈ ʾē=t-d-⁺ṱlàˈ ⁺málla mə̀tlə.ˈ nàšə,ˈ
 xuyravàtuˈ xə́šlun tílun mə̀rrunˈ ʾa mù-vadət? k̭a-mú=ivət ⁺tàmma?ˈ mə́rrə 
 xob-ʾána mìtən.ˈ lá bəxzáyətun k̭at-mìtən!ˈ lá mə́rrun ʾat-xàya!ˈ 
 hamzùməvət.ˈ bəšvák̭una ⁺tàmaˈ màraˈ xmàrələ,ˈ lélə ⁺p̂armùyə.ˈ
```

# Structure

NENA Markup texts consist of two blocks: 1) metadata block, 2) text block.

## Metadata Block

The metadata block contains metadata features and values. Each unique feature
and value is contained on its own line and separated from other feature/values 
by a single line break. 

A single feature/value pair consists of a feature name string, a space, an =
sign, another space, and the value string. **NB: The spaces around = are mandatory**.

```
feature = value
```

The metadata block is ended by a blank line (i.e. two adjacent newline characters).

Obligatory features are: 

* `dialect` - a [valid dialect code](../standards/dialects.json) for this text
* `title` - a unique title for this text
* `encoding` - either `UTF8` or `ASCII` (one-to-one transcription)
* `informant` - the primary speaker in the text

Other valuable features include data about the interviewer, place, 
or transcriber. 

## Text Block

The text block contains the body of the transcribed text. The text must be 
written in one of two encodings: `UTF8` or `ASCII`. Either encodings must 
be written using [valid canonical letters](../standards/alphabet.json), 
[valid punctuation](../standards/punctuation.json), and valid markup strings 
(as defined in this document). 

### Canonical Letters

We draw a distinction between "characters" and "letters". A "character" is a 
technical term for a unique unicode codepoint with very many combination
possibilities (e.g. diacritics). A "letter" is a semantic entity that links
a given combination of characters with a single phonological value. NENA canonical 
letters are thus a select subset of all possible character combinations. With 
the exception of foreign words, only this subset is allowed in the text portions 
of a text block. 

Canonical letters exist in one of two encodings: UTF8 or ASCII. 

**UTF8 encoding** consists of anyone of the canonical letters contained in the 
[NENA Alphabet](../standards/alphabet.json). UTF8 letters can be written 
in composed or non-composed form.

**ASCII encoding** consists of one of the letters contained in the 
NENA Alphabet ASCII transcription.

### Foreign Letters

Letters in words [marked as foreign](#Foreign-Language-Tag) are considered
non-canonical and need not match the canonical encodings. They may consist of 
any combination of non-numeric base characters + zero or more diacritics.
Non-canonical foreign letters in ASCII encoded documents are limited to any
combination of transcribable characters.

### Paragraph Structure

Paragraphs are units of text with some kind of thematic cohesion. Paragraphs 
are delineated by a single blank line (two newline characters). For example:

```
This is
one paragraph.

This is another paragraph.
```

### Punctuation

Any one of the [punctuation characters](../standards/punctuation.json). For ease-of-input, 
the following substituted values are allowed:

| punctuation | substitution |
| ----------- | ------------ |
| ⁺           | +            |
| ˈ           | \|           |

### Span Tags

A span is simply a stretch of text with associated metadata. The metadata
indicated by a span remains "active" for all words which follow it until
a given metadata value is updated by a subsequent span. 

There are currently 3 types of spans:

    * line numbers - verse-like reference numbers, from publications if applicable, or made new if not
    * time stamp - indicates time position of spoken text in an audio file, indicated by at minimum 2 numbers separated with a colon: 0:05
    * speaker - name or initials of a speaker; if initials, should match initials in "speakers" document metadata

Some examples:

```
(2, 0:05, GK)

# Geoffrey Khan is speaking at 5 seconds in the audio within publication number 2
```

or 

```

(1, 0:00) Here is some text (GK) But here is some more.

# Geoffrey Khan starts speaking within a span of text beginning at 0 seconds in publication line 1.
```

### Foreign Language Tag

NENA texts occasionally contain words or stretches of words spoken in a language
foreign to NENA. These words should be indicated with an opening single angle 
bracket (<), a [valid language code](../standards/foreign_languages.json), a colon, 
the foreign words, and a single closing bracket:

```
This is some NENA. <Du:Dit is niet NENA>
```

Any number of words are allowed in a foreign language tag, but the tag should
not take up a substantial portion of the NENA text.
