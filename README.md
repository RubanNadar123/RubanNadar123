```python
import heapq

class Node:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq

def build_huffman_tree(characters):
    heap = [Node(char, freq) for char, freq in characters.items()]
    heapq.heapify(heap)

    while len(heap) > 1:
        left_child = heapq.heappop(heap)
        right_child = heapq.heappop(heap)

        merged_node = Node(None, left_child.freq + right_child.freq)
        merged_node.left = left_child
        merged_node.right = right_child

        heapq.heappush(heap, merged_node)

    return heap[0]  # Root of the Huffman tree
print("Huffman code for characters: ")
def calculate_average_code_length(node, depth, code=""):
    if node:
        if node.char is not None:
            binary_code = format(depth, 'b').zfill(len(code))
            print(f"{node.char}: {binary_code}")
            return len(code) * characters[node.char]

        left_length = calculate_average_code_length(node.left, depth + 1, code + "0")
        right_length = calculate_average_code_length(node.right, depth + 1, code + "1")

        return left_length + right_length

characters = {'a': 10, 'e': 15, 'i': 12, 'o': 3, 'u': 4, 's': 13, 't': 1}

root = build_huffman_tree(characters)
average_code_length = calculate_average_code_length(root, 0)
avgCharacterCodeLength = average_code_length / sum(characters.values())
print("\nAverage Code Length (Per character):", avgCharacterCodeLength)

print("\nLength Of Huffman Encoded Message:", avgCharacterCodeLength * sum(characters.values()))

```
