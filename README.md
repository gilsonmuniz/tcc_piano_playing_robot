# TCC | Piano Playing Robot

- Conversor de partitura para XML: [github.com/BreezeWhite/oemer](https://github.com/BreezeWhite/oemer)
- Exemplo de partitura em XML: [www.w3.org/2021/06/musicxml40/tutorial/introduction](https://www.w3.org/2021/06/musicxml40/tutorial/introduction/)
- Tocar arquivos **.xml** e **.musicxml** online: [soundslice.com/musicxml-viewer](https://www.soundslice.com/musicxml-viewer/)
- Software para tocar **.musicxml**: [musescore.org/en/download](https://musescore.org/en/download)
- Apresentação do projeto: [bit.ly/PianoPlayingRobot](https://bit.ly/PianoPlayingRobot)

## Estrutura do **XML**
``` xml
<!-- titanic.xml -->

<measure number="1"> <!-- compasso 1 -->
    <attributes>
        <divisions>16</divisions>
        <key>
            <fifths>0</fifths> <!-- (+) sustenidos na armadura de clave -->
        </key>
        <staves>1</staves>
        <clef number="1"> <!-- clave 1 -->
            <sign>G</sign> <!-- sol -->
            <line>2</line> <!-- inicia na linha 2 -->
        </clef>
    </attributes>
    <note> <!-- nota -->
        <pitch>
            <step>F</step> <!-- fá -->
            <alter>0</alter> <!-- (+) sustenido na nota -->
            <octave>4</octave> <!-- oitava 4 -->
        </pitch>
        <duration>8</duration> <!-- duração 8 -->
        <type>eighth</type> <!-- colcheia -->
        <stem>up</stem> <!-- haste subindo -->
        <staff>1</staff>
        <voice>1</voice>
    </note>
    <note>
        <pitch>
            <step>G</step> <!-- sol -->
            <alter>0</alter>
            <octave>4</octave> <!-- oitava 4 -->
        </pitch>
        <duration>8</duration> <!-- duração 8 -->
        <type>eighth</type> <!-- colcheia -->
        <stem>up</stem> <!-- haste subindo -->
        <staff>1</staff>
        <voice>1</voice>
    </note>
</measure>
<measure number="16">
    <note>
        <rest measure="yes"/> <!-- pausa -->
        <duration>24</duration>
        <dot/> <!-- ponto de aumento -->
        <staff>1</staff>
    </note>
</measure>
<measure number="19">
    <!-- ... -->
    <note>
        <pitch>
            <step>B</step>
            <alter>-1</alter> <!-- (-) bemol na nota -->
            <octave>4</octave>
        </pitch>
        <duration>16</duration>
        <type>quarter</type>
        <stem>down</stem>
        <staff>1</staff>
        <voice>1</voice>
    </note>
    <!-- ... -->
<!-- ... -->
```
``` xml
<!-- cidade_maravilhosa.xml -->

<!-- ... -->
<measure number="3">
    <note>
        <pitch>
            <step>E</step>
            <alter>0</alter>
            <octave>5</octave>
        </pitch>
        <duration>32</duration>
        <type>half</type>
        <stem>down</stem>
        <staff>1</staff>
        <voice>1</voice>
    </note>
    <note>
        <chord/> <!-- acorde com a última nota -->
        <pitch>
            <step>C</step>
            <alter>0</alter>
            <octave>5</octave>
        </pitch>
        <duration>32</duration>
        <type>half</type>
        <stem>down</stem>
        <staff>1</staff>
        <voice>1</voice>
    </note>
</measure>
<!-- ... -->

```

## Estrutura do **XLSX**
Após ser executado o script Python para tradução do arquivo XML, é gerada uma tabela que contém 3 colunas, que será lida pelo microcontrolador.
Cada linha da matriz, representa uma nota a ser tocada na música, sendo representada pelas 3 células que a definem: **Step**, **Octave**, **Chord** e **Duration**.
- **Step** define a [cifra](https://pt.wikipedia.org/wiki/Cifra_(música)), podendo ser acrescentado **'#'** ou **'b'** após a letra, para indicar [sustenido](https://pt.wikipedia.org/wiki/Sustenido) e [bemol](https://pt.wikipedia.org/wiki/Bemol), respectivamente;
- **Octave** representa a [oitava](https://pt.wikipedia.org/wiki/Oitava);
- **Chord** indica se a nota compõe um [acorde](https://pt.wikipedia.org/wiki/Acorde);
- **Duration** é o tempo de duração da nota.

Exemplo de tabela gerada:

| Step | Octave | Chord | Duration |
|------|--------|-------|----------|
| G    | 4      | false | 8        |
| G    | 4      | false | 4        |
| G    | 4      | false | 4        |
| G    | 4      | false | 16       |
| G    | 4      | false | 8        |
| C    | 5      | false | 8        |
| E    | 5      | false | 32       |
| C    | 5      | true  | 32       |
| Eb   | 5      | false | 24       |
| C#   | 5      | true  | 24       |
| R    | -      | -     | 8        |
| A    | 4      | false | 8        |


## Tipos de nota
<img src="docs\notes-values.png" width="260">