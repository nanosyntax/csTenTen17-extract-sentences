# csTenTen17-extract

Fast CLI tool to extract plain text from the [csTenTen17](http://hdl.handle.net/11234/1-4835) dataset.

> The Czech Web Corpus 2017 (csTenTen17) is a Czech corpus made up of texts collected from the Internet, mostly from the Czech national top level domain ".cz".

**Documents containing unescaped HTML entities might fail to parse.**

## Usage

```bash
csTenTen17-extract -i csTenTen17.vert -o out.txt -n 100
```

* `-i`: Path to the input file
* `-o`: Path to the output file
* `-n`: Number of documents to parse

## Parsing

The parser utilizes a fixed-sized stack, which encodes different parsing states.
Documents are skipped if an invalid state is encountered.

* `[0][0][0]`: Initial state
* `[n][0][0]`: Parsing document contents
* `[n][m][0]`: Parsing paragraph contents
* `[n][m][l]`: Parsing sentence contents

**State transitions are based on the following assumptions.**

A document block always contains at least one paragraph. A paragraph always contains one or more sentences.
Paragraphs cannot be nested. Glue indicators appear only inside sentences. All words come with morphological
information.

## License

MIT
