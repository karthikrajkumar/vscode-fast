# BigCode.Classify - a Visual Studio Code extension for Algorithm Classification using [flattened AST](http://oro.open.ac.uk/59268/).

The Neural Networks supported are currently [Gated Graph Neural Networks](https://arxiv.org/abs/1511.05493)
and [Tree-Based Convolutional Neural Networks](https://arxiv.org/abs/1409.5718).

[![Screencast](https://img.youtube.com/vi/VV2eDDyprmM/0.jpg)](https://www.youtube.com/watch?v=VV2eDDyprmM "Screencast")

## Installation
Before using the extension, you need to save the following file to
an executable bash script `fast` to a folder on the search path.
The `fast` command can pull the docker image of `fast` if it has not been installed,
then pass on the arguments to be processed by the docker image.
```bash
#!/bin/bash
docker pull yijun/fast
docker run --rm -v "$(pwd)":/e yijun/fast $@
```

## Usage
1. Open a C++ or Java program in the editor;

2. Press ⌘ + ⇧ + P,  which will open a "Configuration" window that lists the pre-trained models of neural networks;

INFO. You can also list these models using the following command in the terminal:
```bash
fast model
```

INFO. You can also assign a key binding to this command by Code > Preferences > Keyboard Shortcuts or by adding the following to your `keybindings.json` file:
```json
[
    {
        "key": "ctrl+b ctrl+c",
        "command": "BigCode.Classify"
    }
]
```

3. Select a pre-trained model from the "Model:" drop-down list in the "Configuration" window, which will generate an HTML file to be opened in a WebView window as a tab next to the code editor. After the selection, try not to move your
mouse away so it will open the HTML page after a few seconds.

INFO. The colors of the tokens are assigned according to the attention score of the token for the neural network to predict the classification. 
The closer it is on the spectrum to Red, the more important (red score = 1); the closer it is on the spectrum to the
background color (e.g., white), the less important it is (white score = 0). For your information, this spectrum is called Hue-Saturation-Brightness in the HSB color scheme. The token colors follow the hue, saturation, and brightness (HSB) spectrum, with full saturation=1 and brightness=1. The hue is a color analogous to the hotness, where background = 0 to red = 1, and any color in-between is determined by the attention score. 


INFO. The title of the WebView tab is named after the source code file, annotated with a number indicating which model was selected to generate the attention scores.

INFO. At the end of the webview, you can see the classification results, i.e., the probabilities of the current program belong to each class. According to our Dataset 1 of 10 sorting problems, collected from Github, the meaning of a class is the following: 
```
0 insertion-sort
1 merge-sort
2 topological-sort
3 heap-sort
4 bubble-sort
5 radix-sort
6 shell-sort
7 quick-sort
8 selection-sort
9 bucket-sort
```
A PNG image file generated highlights the predicted label in blue if it is correct, or red if it is wrong, 
amongst the probability distribution (10 bars).

4. Select another pre-trained model from the "Configuration" window, another tab will be shown after a few seconds, which highlights different tokens in the code due to the change of the attention scores.

5. You can rearrange the tabs to compare and contrast the effect of the visualizations.

## Datasets 

Dataset 1: 10 sorting problems, collected from Github [Bui et al. SANER'19, NL4SE@AAAI'18], which are insertion-sort, merge-sort, topological-sort, heap-sort, bubble-sort, radix-sort, shell-sort, quick-sort, selection-sort, bucket-sort.

Dataset 2: 104 programming tasks at Peking University [Mou et al. AAAI'16], which comprises of 52000 cpp files from the paper Convolutional Neural Networks over Tree Structures for Programming Language Processing, AAAI 2015.

## References

Nghi D. Q. BUI, Yijun YU, Lingxiao JIANG. "[Bilateral Dependency Neural Networks for Cross-Language Algorithm Classification](https://bdqnghi.github.io/files/SANER_2019_bilateral_dependency.pdf)", In the 26th edition of the IEEE International Conference on Software Analysis, Evolution and Reengineering, Research Track, Hangzhou, China, February 24-27, 2019.

Nghi D. Q. BUI, Lingxiao JIANG, and Yijun YU. "[Cross-Language Learning for Program Classification Using Bilateral Tree-Based Convolutional Neural Networks](https://bdqnghi.github.io/files/AAAI_18_cross_language_learning.pdf)", In the proceedings of the 32nd AAAI Conference on Artificial Intelligence (AAAI) Workshop on NLP for Software Engineering, New Orleans, Louisiana, USA, 2018.

Miltiadis Allamanis, Marc Brockschmidt, Mahmoud Khademi. "[Learning to Represent Programs with Graphs](https://arxiv.org/abs/1711.00740)", In: 6th International Conference on Language Representations (ICLR), 2018.

Y Li, D Tarlow, M Brockschmidt, R Zemel. "[Gated graph sequence neural networks](https://arxiv.org/abs/1511.05493)", In: 4th International Conference on Language Representations (ICLR), 2016.

Lili Mou, Ge Li, Lu Zhang, Tao Wang, Zhi Jin: "[Convolutional Neural Networks over Tree Structures for Programming Language Processing](https://arxiv.org/abs/1409.5718)". In: AAAI 2016: 1287-1293
