# mm2md
Convert FreeMind to Markdown. Created by ChatGPT

Colab: https://colab.research.google.com/drive/1vQba6WMsr4n4pHyHtZ9Bx785hIQaPcVv?usp=sharing

```python
import xml.etree.ElementTree as ET
import sys

# print the extracted text data
print('---')
print('markmap:')
print('  colorFreezeLevel: 2')
print('---')

def print_node(node, visited_nodes, indent_level=0):
    indent = '  ' * indent_level
    text = node.attrib.get('TEXT', '').strip()
    if node.tag == 'node' and 'id' in node.attrib:
        print(f'{indent}- {text}')
        print(f'{indent}  id: {node.attrib["id"]}')
    else:
        print(f'{indent}- {text}')
    for child_node in node.iter():
        if child_node in visited_nodes:
            continue
        visited_nodes.add(child_node)
        print_node(child_node, visited_nodes, indent_level+1)

import xml.etree.ElementTree as ET

# parse the XML file
tree = ET.parse('ComputerVision.mm')
root = tree.getroot()
visited_nodes = set()
for child_node in root:
    visited_nodes.add(child_node)
    print_node(child_node, visited_nodes)
```
