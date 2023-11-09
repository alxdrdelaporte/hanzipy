# Hanzipy
<p align="center">
    <a href="https://circleci.com/gh/Synkied/hanzipy">
        <img src="https://circleci.com/gh/Synkied/hanzipy.svg?style=svg" alt="TravisCI Build Status"/>
    </a>
</p>


Hanzipy is a Chinese character and NLP module for Chinese language processing for python.  
It is primarily written to help provide a framework for Chinese language learners to explore Chinese.  
It was translated from the awesome library provided by nieldlr: https://github.com/nieldlr/hanzi

The following README is copy/pasted from the above repository but adapted for the python language.

At present features include:

- Character decomposition into components
- Dictionary definition lookup using CC-CEDICT
- Phonetic Regularity Computation
- Example Word Calculations

Future features planned:

- Futur plans to include IDS: https://github.com/cjkvi/cjkvi-ids

Currently the data was generated by Gavin Grover
http://groovy.codeplex.com/wikipage?title=cjk-decomp

## Install

```python
pip install hanzipy
```

## How to use

### Initiate Hanzipy. Required.

```python
# import decomposer
from hanzipy.decomposer import HanziDecomposer
decomposer = HanziDecomposer()
# import dictionary
from hanzipy.dictionary import HanziDictionary
dictionary = HanziDictionary()

```

hanzipy has been seperated into two different modules for clarity purposes.
The `decomposer` aims to focus on character or phrase decomposition.
The `dictionary` is has the name implies, focused on providing dictionary entries and phrase examples.

### Hanzi Dictionary

#### dictionary.definition_lookup(character/word, script_type=None)

Returns a dictionary entry object. ```script_type``` is optional.

```script_type``` parameters:

- "simplified" - Simplified
- "traditional" - Traditional

```python
print(dictionary.definition_lookup("雪"))

[
    {
        "traditional": "雪",
        "simplified": "雪",
        "pinyin": "Xue3",
        "definition": "surname Xue",
    },
    {
        "traditional": "雪",
        "simplified": "雪",
        "pinyin": "xue3",
        "definition": "snow/CL:場|场[chang2]/(literary) to wipe away (a humiliation etc)",  # noqa
    },
]

print(dictionary.definition_lookup("這", "traditional"))
[
    {
        "traditional": "這",
        "simplified": "这",
        "pinyin": "zhe4",
        "definition": "this/these/(commonly pr. [zhei4] before a classifier, esp. in Beijing)",
    }
]
```

#### dictionary.dictionary_search(characters, search_type=None)

Searches the dictionary based on input. ```search_type``` changes what data it returns. Defaults to None.

```search_type``` parameters:

- "only" - this parameter returns only entries with the characters specfied. This is a means to find all compounds words with the characters specified.
- None - returns all occurences of the character.

```python
print(dictionary.dictionary_search("雪"))

[
    {
        "traditional": "一雪前恥",
        "simplified": "一雪前耻",
        "pinyin": "yi1 xue3 qian2 chi3",
        "definition": "to wipe away a humiliation (idiom)",
    },
    {
        "traditional": "下雪",
        "simplified": "下雪",
        "pinyin": "xia4 xue3",
        "definition": "to snow",
    },
    {
        "traditional": "伸雪",
        "simplified": "伸雪",
        "pinyin": "shen1 xue3",
        "definition": "variant of 申雪[shen1 xue3]",
    },
    {
        "traditional": "似雪",
        "simplified": "似雪",
        "pinyin": "si4 xue3",
        "definition": "snowy",
    },
    {
        "traditional": "冰天雪地",
        "simplified": "冰天雪地",
        "pinyin": "bing1 tian1 xue3 di4",
        "definition": "a world of ice and snow",
    },
    {
        "traditional": "冰雪",
        "simplified": "冰雪",
        "pinyin": "bing1 xue3",
        "definition": "ice and snow",
    },
    {
        "traditional": "冰雪皇后",
        "simplified": "冰雪皇后",
        "pinyin": "Bing1 xue3 Huang2 hou4",
        "definition": "Dairy Queen (brand)",
    },
    {
        "traditional": "冰雪聰明",
        "simplified": "冰雪聪明",
        "pinyin": "bing1 xue3 cong1 ming5",
        "definition": "exceptionally intelligent (idiom)",
    },
    {
        "traditional": "各人自掃門前雪，莫管他家瓦上霜",
        "simplified": "各人自扫门前雪，莫管他家瓦上霜",
        "pinyin": "ge4 ren2 zi4 sao3 men2 qian2 xue3 , mo4 guan3 ta1 jia1 wa3 shang4 shuang1",
        "definition": "sweep the snow from your own door step, don't worry about the frost on your neighbor's roof (idiom)",
    },
    {
        "traditional": "哈巴雪山",
        "simplified": "哈巴雪山",
        "pinyin": "Ha1 ba1 xue3 shan1",
        "definition": "Mt Haba (Nakhi: golden flower), in Lijiang 麗江|丽江, northwest Yunnan",
    },
    {
        "traditional": "單板滑雪",
        "simplified": "单板滑雪",
        "pinyin": "dan1 ban3 hua2 xue3",
        "definition": "to snowboard",
    },
    {
        "traditional": "報仇雪恥",
        "simplified": "报仇雪耻",
        "pinyin": "bao4 chou2 xue3 chi3",
        "definition": "to take revenge and erase humiliation (idiom)",
    },
    {
        "traditional": "報仇雪恨",
        "simplified": "报仇雪恨",
        "pinyin": "bao4 chou2 xue3 hen4",
        "definition": "to take revenge and wipe out a grudge (idiom)",
    },
]
[....] # Truncated for display purposes

print(dictionary.dictionary_search("心的小孩真", "only"))

[
    {"traditional": "孩", "simplified": "孩", "pinyin": "hai2", "definition": "child"},
    {
        "traditional": "小",
        "simplified": "小",
        "pinyin": "xiao3",
        "definition": "small/tiny/few/young",
    },
    {
        "traditional": "小孩",
        "simplified": "小孩",
        "pinyin": "xiao3 hai2",
        "definition": "child/CL:個|个[ge4]",
    },
    {
        "traditional": "小小",
        "simplified": "小小",
        "pinyin": "xiao3 xiao3",
        "definition": "very small/very few/very minor",
    },
    {
        "traditional": "小心",
        "simplified": "小心",
        "pinyin": "xiao3 xin1",
        "definition": "to be careful/to take care",
    },
    {
        "traditional": "小的",
        "simplified": "小的",
        "pinyin": "xiao3 de5",
        "definition": "I (when talking to a superior)",
    },
    {
        "traditional": "心",
        "simplified": "心",
        "pinyin": "xin1",
        "definition": "heart/mind/intention/center/core/CL:顆|颗[ke1],個|个[ge4]",
    },
    {
        "traditional": "的",
        "simplified": "的",
        "pinyin": "de5",
        "definition": "of/~'s (possessive particle)/(used after an attribute)/(used to form a nominal expression)/(used at the end of a declarative sentence for emphasis)/also pr. [di4] or [di5] in poetry and songs",
    },
    {
        "traditional": "的",
        "simplified": "的",
        "pinyin": "di1",
        "definition": "see 的士[di1 shi4]",
    },
    {
        "traditional": "的",
        "simplified": "的",
        "pinyin": "di2",
        "definition": "really and truly",
    },
    {"traditional": "的", "simplified": "的", "pinyin": "di4", "definition": "aim/clear"},
    {
        "traditional": "真",
        "simplified": "真",
        "pinyin": "zhen1",
        "definition": "really/truly/indeed/real/true/genuine",
    },
    {
        "traditional": "真心",
        "simplified": "真心",
        "pinyin": "zhen1 xin1",
        "definition": "sincere/heartfelt/CL:片[pian4]",
    },
    {
        "traditional": "真真",
        "simplified": "真真",
        "pinyin": "zhen1 zhen1",
        "definition": "really/in fact/genuinely/scrupulously",
    },
]


```

#### dictionary.get_examples(character)

This function does a dictionary_search(), then compares that to the Leiden University corpus for vocabulary frequency, then sorts the dictionary entries into three categories in an array: [high frequency, medium frequency and low frequency].

The frequency categories are determined relative to the frequency distribution of the dictionary_search data compared to the corpus.

```python
print(dictionary.get_examples("橄"))

{
    "high_frequency": [
        {
            "traditional": "橄欖",
            "simplified": "橄榄",
            "pinyin": "gan3 lan3",
            "definition": "Chinese olive/olive",
        },
        {
            "traditional": "橄欖油",
            "simplified": "橄榄油",
            "pinyin": "gan3 lan3 you2",
            "definition": "olive oil",
        },
    ],
    "mid_frequency": [
        {
            "traditional": "橄欖球",
            "simplified": "橄榄球",
            "pinyin": "gan3 lan3 qiu2",
            "definition": "football played with oval-shaped ball (rugby, American football, Australian rules etc)",
        },
        {
            "traditional": "橄欖綠",
            "simplified": "橄榄绿",
            "pinyin": "gan3 lan3 lu:4",
            "definition": "olive-green (color)",
        },
    ],
    "low_frequency": [
        {
            "traditional": "橄欖枝",
            "simplified": "橄榄枝",
            "pinyin": "gan3 lan3 zhi1",
            "definition": "olive branch/symbol of peace",
        },
        {
            "traditional": "橄欖樹",
            "simplified": "橄榄树",
            "pinyin": "gan3 lan3 shu4",
            "definition": "olive tree",
        },
        {
            "traditional": "橄欖石",
            "simplified": "橄榄石",
            "pinyin": "gan3 lan3 shi2",
            "definition": "olivine (rock-forming mineral magnesium-iron silicate (Mg,Fe)2SiO4)/peridot",
        },
    ],
}
```

<!-- #### hanzi.segment(phrase) - NOT YET AVAILABLE

Returns an array of characters that are segmented based on a longest match lookup.

````python
print(hanzi.segment("我們都是陌生人。"))

["我們", "都", "是", "陌生人", "。"]
```` -->

#### dictionary.get_pinyin(character)

Returns all possible pinyin data for a character.

```python
print(dictionary.get_pinyin("的"))

["de5", "di1", "di2", "di4"]
```

#### dictionary.get_character_frequency(character)

Returns frequency data for a character based on the Junda corpus. The data is in simplified characters, but I made the function script agnostic. So both traditional and simplified will return the same data.

```python
print(dictionary.get_character_frequency("热"))

{
    "number": 606,
    "character": "热",
    "count": "67051",
    "percentage": "79.8453694124",
    "pinyin": "re4",
    "meaning": "heat/to heat up/fervent/hot (of weather)/warm up",
}
```

#### dictionary.get_character_in_frequency_list_by_position(position)

Gets a character based on its position the frequency list. This only goes up to 9933 based on the Junda Frequency list.

```python
print(dictionary.get_character_in_frequency_list_by_position(111))

{
    "number": 111,
    "character": "机",
    "count": "339823",
    "percentage": "43.7756134862",
    "pinyin": "ji1",
    "meaning": "machine/opportunity/secret",
}
```

#### dictionary.determine_phonetic_regularity(decomposition_object/character)

This function takes a decomposition object created by hanzipy.decompose() or a character, then returns an object that displays all possible combinations of phonetic regularity relationship of the character to all its components.

Phonetic Regularity Scale:

- 0 = No regularity
- 1 = Exact Match (with tone)
- 2 = Syllable Match (without tone)
- 3 = Similar in Initial (alliterates)
- 4 = Similar in Final (rhymes)

The object returned is organized by the possible pronunciations of the character. You may notice duplicate entries in the fields, but these are there based on the similarities between the decomposition levels. It is up to the developer to use this data or not.

```python
print(dictionary.determine_phonetic_regularity("洋"))

{
    "yang2": {
        "character": "洋",
        "component": ["氵", "羊", "羊", "氵", "羊", "羊"],
        "phonetic_pinyin": [
            "shui3",
            "Yang2",
            "yang2",
            "shui3",
            "Yang2",
            "yang2",
        ],
        "regularity": [0, 1, 1, 0, 1, 1],
    }
}

```

### Hanzi Decomposer

#### decomposer.decompose(character, decomposition_type=None)

A function that takes a Chinese character and returns an object with decomposition data. Type of decomposition is optional.

Type of decomposition levels:

- 1 - "Once" (only decomposes character once),
- 2 - "Radical" (decomposes character into its lowest radical components),
- 3 - "Graphical" (decomposes into lowest forms, will be mostly strokes and small indivisable units)

```python
decomposition = decomposer.decompose("爱")
print(decomposition)

{
    "character": "爱",
    "once": ["No glyph available", "友"],
    "radical": ["爫", "冖", "𠂇", "又"],
    "graphical": ["爫", "冖", "𠂇", "㇇", "㇏"],
}

# Example of forced level decomposition

decomposition = hanzi.decompose("爱", 2)
print(decomposition)

{"character": "爱", "components": ["爫", "冖", "𠂇", "又"]}
```

#### decomposer.decompose_many(character string, type of decomposition)

A function that takes a string of characters and returns one object for all characters.

```python
decomposition = hanzi.decompose_many("爱橄黃")
print(decomposition)

{
    "爱": {
        "character": "爱",
        "once": ["No glyph available", "友"],
        "radical": ["爫", "冖", "𠂇", "又"],
        "graphical": ["爫", "冖", "𠂇", "㇇", "㇏"],
    },
    "橄": {
        "character": "橄",
        "once": ["木", "敢"],
        "radical": ["木", "No glyph available", "耳", "⺙"],
        "graphical": ["一", "丨", "八", "匚", "二", "丨", "二", "丿", "一", "乂"],
    },
    "黃": {
        "character": "黃",
        "once": ["廿", "No glyph available"],
        "radical": ["黃"],
        "graphical": ["卄", "一", "一", "二", "丨", "凵", "八"],
    },
}
```

#### decomposer.component_exists(character/component)

Check if a component/character exists in the data. Returns boolean value.

```python
print(decomposer.component_exists("乂"))

True

print(decomposer.component_exists("$"))

False
```

#### decomposer.get_characters_with_component(component)

Returns an array of characters with the given component. If a component has bound forms, such as 手 and 扌, they"re considered the same and returns all the characters with the component.

NB: This feature is new. Data might not be hundred percent correct and consistent.

```python
print(decomposer.get_characters_with_component("囗"))

["国","因","西","回","口","四","团","图","围","困","固","园","圆","圈","囚","圃","囤","囿","囡","囫","圜","囵","囹","圄","囝","圉","圊","釦"]
```

#### decomposer.get_radical_meaning(radical)

Returns a short, usually one-word, meaning of a radical.

```python
print(decomposer.get_radical_meaning("氵"))

water
```

## Projects

Hanzipy is used in the following projects:

## Contributors

- [synkied (Author)](https://github.com/synkied)

## License

Hanzipy uses data from various sources:

- [CEDICT](http://cc-cedict.org/wiki/)
- [Gavin Grover's Decomposition Data](http://cjkdecomp.codeplex.com/license)
- [Leiden Word Frequency Data](http://lwc.daanvanesch.nl/legal.php)
- [Jun Da Character Frequency Data](http://lingua.mtsu.edu/chinese-computing/copyright.html)

Other data files are either generated by Hanzipy or are not in use at present in the software.
