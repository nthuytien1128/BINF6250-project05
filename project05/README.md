# Introduction
This project focuses on implementing the Smith–Waterman algorithm, a dynamic programming method used for local sequence alignment in bioinformatics. Pairwise sequence alignment is an essential technique used to compare biological sequences such as DNA, RNA, or proteins to identify regions of similarity that may indicate functional, structural, or evolutionary relationships.

The Smith–Waterman algorithm improves efficiency compared to brute-force sequence alignment methods. Instead of evaluating every possible alignment, it uses dynamic programming to build a scoring matrix and reuse previously computed results. This reduces the computational complexity to O(mn) for sequences of length m and n.

In this project, we implemented the algorithm in Python by completing several components:

Scoring matrix calculation (cal_score)
Computes the score for each cell in the dynamic programming matrix using match, mismatch, and gap penalties. The score is calculated based on the maximum of:

diagonal (match or mismatch)

up (gap in sequence 2)

left (gap in sequence 1)

zero (for local alignment reset)

Traceback function (traceback)
Reconstructs the optimal local alignment by tracing back from the highest scoring cell in the matrix until the algorithm reaches an end condition.

Smith–Waterman driver function (smith_waterman)
Initializes the scoring and traceback matrices, fills them using dynamic programming, identifies the maximum score location, and performs traceback to produce the final aligned sequences.

The implementation allows customizable scoring parameters including match score, mismatch penalty, and gap penalty.

# Pseudocode
Put pseudocode in this box:

```
Smith-Waterman Algorithm:

Call scoring function to create matrix and get position of best score

    Initialize matrix with zeroes (use np.zeros(i,j)) --> i is rows (len(seq1)), j is columns (len(seq2))
    
    Iterate through each position (walk through each row) and call scoring function (exclude first row and columm)

    Update matrices with score and traceback move for that position

Find max value in matrix --> find argmax and unravel to get coordinates

Call traceback function with recorded moves to get aligned seqs & score

Print aligned sequences and the alignment score

Calculate Score:
Check if seqs match or mismatch at position (i, j) --> string evaluation

Create dictionary {'0-END': 0, '1-DIAG': 0, '2-UP': 0, '3-LEFT': 0} to track moves and scores

Calculate diagonal score

    Take score at matrix(i-1, j-1)

    If we have a match --> add match value to score

    Else --> add mismatch value to score

Calculate up score

    Take score at matrix(i-1, j) and add gap value

Calculate left score

    Take score at matrix(i, j-1) and add gap value

Take max value as score

Return score and direction of that score (we can use the dictionary)

Traceback:
Start at max position

Identify starting bases for seq1 (maximum_position[0]) and seq2 (maximum_position[2])

Access move in traceback_matrix using maximum_position

Iterate through each of the moves until we end at a "END" move (while loop)

    current_position (row, column)
    current_move (string)

    If curent move is DIAG

        Extend aligned_seq1 with the corresponding base from seq1 (seq1[row])
        Extend aligned_seq2 with the corresponding base from seq2 (seq2[column])
        Update current_position to matrix[row-1, column-1]

    If current move is UP

        Extend aligned_seq1 with the corresponding base from seq1 (seq1[row])
        Extend aligned_seq2 with - (vertical gap)
        Update current_position to matrix[row-1, column]

    If current move is LEFT

        Extend aligned_seq1 with - (horizontal gap)
        Extend aligned_seq2 with the corresponding base from seq2 (seq2[column])
        Update current_position to matrix[row, column-1]

Reverse aligned_seqs (so they are in order)

Return the aligned sequences 
```

# Successes
Our team was able to successfully implement the Smith–Waterman algorithm according to the requirements in the notebook. Working collaboratively allowed us to divide the problem into manageable parts and verify each step of the algorithm. Starting early and meeting during Spring Break helped us stay organized and make steady progress.

One major success was correctly implementing the dynamic programming scoring matrix, which required understanding how each cell depends on the neighboring cells. Once the scoring logic was working, implementing the traceback process to reconstruct the optimal alignment became clearer. By the end of the project, we were able to generate aligned sequences and verify that our results matched the expected outputs.

Another positive aspect of this project was that we did not have to deal with large-scale memory or scaling issues, which allowed us to focus more on understanding the algorithm itself rather than optimizing performance.

# Struggles
The main challenge at the beginning of the project was understanding how the different functions interacted with each other. Initially, it was difficult to fully grasp how the scoring matrix, traceback matrix, and alignment reconstruction worked together within the dynamic programming framework.

Another difficulty was managing matrix indexing and traceback directions, since the algorithm requires careful tracking of diagonal, up, and left moves while building the alignment. Small indexing mistakes could easily produce incorrect alignments.

However, as we progressed through the implementation—especially when working on the traceback and smith_waterman functions—the logic became clearer. Breaking the problem into smaller components and testing each function helped us overcome these challenges.

# Personal Reflections
## Tien Nguyen
Working with Marcos and Spencer was very effective. We were able to start the project early and even met during Spring Break to work on it together. Compared to the previous project, this one was easier to understand. One positive aspect was that we did not have to deal with scaling and memory issues.

At first, I struggled to understand how the functions worked, but it became clearer as we progressed, especially when we reached the traceback and smith_waterman functions. Overall, I believe we successfully completed the project according to the requirements outlined in the notebook.

## Marcos Equiza Gasco
Overall I think this project was a bit easier to implement than the last few ones. I feel like the algorithm was pretty straight-forward, and the implementation allowed us to experiment with numpyand matrices. Working with Tien and Spencer was very easy, as they were very responsive and we were able to start early. We implemented a dictionary to track scores in the scoring function, which was very useful, as we were able to simply call the max() function to get our desired values. We had a few struggles with the indices for our sequences, as the scoring and traceback matrices were one row and one column larger than the sequences, but once we realized that it was easy to manage.

## Spencer Todd
This project went smoothly and the team was able to collaborate and implement the algorithm in a manner that felt satisfactory. I found the biggest success working with Tien and Marcos was the meetings were highly efficient. Our initial meeting started with everyone getting on the same page conceptually, and future meetings transitioning to in-session code writing. Similarly to the previous project on De Bruijn graphs, I personally struggled with understanding how we would translate the algorithm into code, since my conceptual understanding of the algorithm was mainly visual. However, this was overcome with strong teammates!
# Generative AI Appendix
As per the syllabus
None was used
