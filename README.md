# StructuringMagic
## Towards a Digital Infrastructure of Texts and Artefacts

* when: 20 - 24 February 2023
* where: Lorentz Center@Snellius

TEI Customazing [Schema](https://kollatzthomas.github.io/StructuringMagic/schema/tei_magic.html) for Structuring Magic across projects. 

### A proposal 

Firstly, this **proposal for Structuring Magic** customizes the TEI-Element `seq` – (arbitrary segment) represents any segmentation of text below the ‘chunk’ level – and defines the following two attributes: 
* `type` characterizes the element in some sense, using any convenient classification scheme or typology. 
    - `list` sequence: any kind of lister; number of elements could be specified by n
    - `formula` formula: any kind of formulae
    - `undefined` i.e. segment that is currently undefined: to be discussed
    - … more values to be discussed and then added
*  `ana` (analysis) indicates one or more elements containing interpretations of the element on which the ana attribute appears. 
    -  `voces_magicae` unit or object can somehow understood as voces
    -  `characteres`
    -  `formulae`
    -  `temporal`
    -  `spatial`
    -  … more values to be discussed and then added

Secondly, the TEI-Element `rs` – (referencing string) reference string used to encode all kind of entities (persons, places, events, terms, etc.) – is customized with the following values for the attribute `type`:
    - `person` referring to any kind of person or being (supranatural or human)
    - `place`
    - `formula`
    - `ritual_practice`
    - `medium`
    - … more values to be discussed and then added
    
### examples
1. [test01.xml](https://github.com/KollatzThomas/StructuringMagic/blob/main/objects/test/test01.xml)
```xml
<ab>
    <seg type="list" xml:lang="gr" ana="characteres"><lb/>(Greek letters+magic charaktéres)
      <lb/>(Greek letters+magic charaktéres)
      <lb/>(Greek letters+magic charaktéres)</seg>
      <lb/>[Guar]d <rs type="person">Ada son of Marthana</rs>, <seg type="formula">Amen, Amen, Selah</seg>.
      <lb/><seg type="list" subtype="names_divine">[In the name ofl God, the holy, our God, the God, our God, the God of hosts</seg> -
      <lb/>[...]swr) )brtn hyd 	)brtn wb) dymnhmnws
      <lb/>[...]t) qq ddwsh )nnwn )nwtw )ggn bryh 1b
      <lb/>[...] 	)dwnh)  s)lm smslm
      <lb/>[...]t )qr) m)kh mry )bln) tn)lb) 
      <lb/>[ ] 	mrbb)l )str) qpqh - redeem
      <lb/>[and] guard <rs type="person">Ada son of Marthana</rs> from every evil <rs>pain</rs>,
            Amen.
      <lb/>d[w]qwn dyqwn dyqnwn )ystrqtwn. In the name of the <rs type="person" subtype="supranatural" n="7">seven holy
      <lb/>angels</rs> which every spirit and plague-demons are given in their hands, I adjure
      <lb/>against a spirit that comes upon Ada son of Marthana that you shall not  harm him, that where[ever]
      <lb/>these names will be read (any spirit) will not remain. I write (it) and (then) the fever will be eradicated.
      <lb/><seg type="list">(magic charaktéres)</seg>         
</ab>
```
2. [test02.xml](https://github.com/KollatzThomas/StructuringMagic/blob/main/objects/test/test02.xml)
```xml
<ab>
    <rs type="person" xml:id="A">I</rs> demand from <rs type="person" xml:id="B" corresp="#A">you</rs>,
according to your promises in front of the fire, <seg type="list" ana="temporal" n="3">at once, today,
right now,</seg> enter into N daughter of N as <rs type="medium">fire</rs> and as a <rs type="medium">flame</rs>,
so that she will <seg n="3">neither eat, nor drink, nor get up</seg> until sees N son of N.
<seg type="formula" n="2">Amen. Amen.</seg>        
</ab>
```

### How to use in your project
1. Embed the `tei_magic.rng` in your XML-Document
```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="https://raw.githubusercontent.com/KollatzThomas/StructuringMagic/refs/heads/main/schema/tei_magic.rng" type="application/xml" schematypens="http://relaxng.org/ns/structure/1.0"?>
<?xml-model href="https://raw.githubusercontent.com/KollatzThomas/StructuringMagic/refs/heads/main/schema/tei_magic.rng" type="application/xml"
	schematypens="http://purl.oclc.org/dsdl/schematron"?>
```
2. Embed the following sequence in the ODD of your project, which specifies the `seq` and the `rs` elements:
([tei_magic.odd](https://github.com/KollatzThomas/StructuringMagic/blob/main/schema/tei_magic.odd))
```xml
<elementspec ident="seg" mode="change">
    <attlist>
        <attdef ident="ana" mode="change">
            <vallist type="closed" mode="change">
                <valitem ident="voces_magicae">
                    <desc xml:lang="en">unit or object can somehow understood as
                        voces</desc>
                </valitem>
                <valitem ident="characteres">
                    <desc></desc>
                </valitem>
                <valitem ident="formulae">
                    <desc></desc>
                </valitem>
                <valitem ident="temporal">
                    <desc></desc>
                </valitem>
                <valitem ident="spatial">
                    <desc></desc>
                </valitem>
            </vallist>
        </attdef>
        <attdef ident="type" mode="change">
            <vallist type="closed" mode="replace">
                <valitem ident="list">
                    <desc xml:lang="en">sequence: any kind of lister; number of elements
                        could be specified by <att>n</att></desc>
                </valitem>
                <valitem ident="formula">
                    <desc xml:lang="en">formula: any kind of formulae</desc>
                </valitem>
                <valitem ident="undefined">
                    <desc xml:lang="en">segment that is currently undefined: to be
                        discussed</desc>
                </valitem>
            </vallist>
        </attdef>
    </attlist>
</elementspec>
<elementspec ident="rs" mode="change">
    <desc xml:lang="en">reference string used to encode all kind of entities (persons,
        places, events, terms, etc.)</desc>
    <!-- use rs for all kind of entities -->
    <attlist>
        <attdef ident="type" mode="change">
            <!-- @type for unique attributions -->
            <vallist type="closed" mode="change">
                <valitem ident="person">
                    <desc xml:lang="en">referring to any kind of person or being
                        (supranatural or human)</desc>
                </valitem>
                <valitem ident="place">
                    <desc></desc>
                </valitem>
                <valitem ident="formula">
                    <desc></desc>
                </valitem>
                <valitem ident="ritual_practice">
                    <desc></desc>
                </valitem>
                <valitem ident="medium">
                    <desc></desc>
                </valitem>
            </vallist>
        </attdef>
    </attlist>
</elementspec>
```

## Future Steps
This is a proposal! If projects want to use this schema in their projects in order to search for traces of magic across projects these projects should agree on features to be encoded. By doing this it will be possible to ask research questions across corpora.  
