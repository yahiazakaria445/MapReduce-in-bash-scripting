# MapReduce in Bash Scripting

### This project implements a simplified MapReduce framework using pure Bash scripting to count the total number of words in a large file. It demonstrates the fundamental concepts of distributed computing: splitting data, mapping, and reducing all within the shell environment. ###
---

## project architecture diagram


![Untitled-2025-03-22-2328](https://github.com/user-attachments/assets/b80c9808-cef6-41d8-ab56-a9bf6ef292ad)

---

## 📁 directory Structure
```
├── map.sh        Map script: counts words in a chunk   
├── reduce.sh     Reduce script: sums word counts   
├── run.sh        Orchestrates the whole MapReduce flow
├── input/        Contains the original input file    
├── chunks/       Contains split chunks of the input   
├── maps/         Contains outputs from the map step    
└── output/       Final word count result
```
---
## 📁 About the Source File: `/usr/share/dict/words`
This project uses a built-in dictionary file as the input source.
### i knew this file throw The Linux Command Line book by William Shotts  
![1](https://github.com/user-attachments/assets/b31706e6-77c9-4491-b35b-0f4826910187)

- It's a system dictionary file commonly found on Unix-like systems (Linux, macOS).
- Contains a list of English words, typically one word per line.
- Used by programs like spell checkers, word games, or autocomplete tools.
### Why use it here?
- It’s a large, clean, and consistent text file perfect for testing.
- Easy to access without needing to download anything.
- Great for benchmarking word count operations in this MapReduce simulation.

---
## Scripts

###   📄 `run.sh`


-  Ensures the script exits on errors with `set -e`.
-  Creates required directories: `input`, `chunks`, `maps`, `output`.
-  Copies the input text file (`/usr/share/dict/words`) to `input/`.
-  Splits the input file into 4 equal-sized chunks.
-  Runs `map.sh` in parallel on each chunk and stores results in `maps/`.
-  Waits for all mapping processes to finish.
-  Runs `reduce.sh` to sum all word counts from the map outputs.
-  Prints the final word count to the terminal.

###  📄 `map.sh`

-  Accepts a file name as input (from `run.sh`).
-  Uses `wc -w` to count the number of words in that file.
-  Outputs the word count (just a number).
-  Represents a single "Map" task can be run independently on any data chunk.

###  📄 `reduce.sh`

-  Accepts multiple `.out` files (outputs from `map.sh`).
-  Reads the number from each file (each is a word count).
-  Adds all the numbers to get the total word count.
-  Outputs the total to stdout (captured by `run.sh` into `output/total.txt`).
-  Acts as a "Reducer" aggregates results from all mappers.

---
### ▶️ How to Run
Follow these steps to run the Scripts:
```
chmod +x run.sh map.sh reduce.sh

./run.sh
```
![Untitled](https://github.com/user-attachments/assets/7aad4e97-dc71-43f0-a3b3-f3fd629faa44)

This will print the total word count to the terminal and save it in `output/total.txt`

---
