# Introduction
The Viterbi algorithm makes use of Dynamic Programming methods to find the most likely and optimal path to hidden states called “Viterbi Path”.
 
Implementation
In our implementation the first observation is “G”, and the possible hidden states are “I” and “G”. That is going to be from our input. We implemented the log-probabilities, so it added these scores along a path. A higher score means a more probable path.
 
The Viterbi algorithm follows 4 major steps.  
 
Initialization - At index “0”, observation is “G”. For each possible hidden state we are adding its initial log-probability and its log-probability of emitting the observed “g”. Previous state is “None” since that is the first position.
 
Recursion - At every later index, it is calculated the best score for ending in each hidden state. To end in “G” at index “3”, we would need to compare “I” -> “G” transition and “G” -> “G” transition. Where each candidate adds the previous path’s score, the transition log-probability, and the log-probability that “G” emits the observation at index “3”. Since both candidates end in “G”, they use the same emission term. The output shows that “G” -> “G” candidate wins, so “Backpointer[3][“G”]” is “G”. Then we repeat the comparison for paths ending in “I”.
 
Termination - At the last index, “8”, both scores represent paths that cover all nine observations. We pick the stat with higher final score. Which in our case was “G” -> -13.9291 against “I” -> -17.2249.  Showing “G” as the last state of the best path, and the score of the complete path.
 
Backtracing - It stated at “G” at the index “8” and follow one backpointer at a time. At each step, backpointer[index][state] gives you the state a the previous index. When we reach “G” at index “3”, Backpointer[3][“G”] tells to put [“G”] at the index [2]. The “I” score at the index [2] was higher for the first three observations, but the best part through all nine traces back though “G” there. Reverse the collected states to return them in observation order.
 
The final output on the project input is:
 
['G', 'G', 'G', 'G', 'G', 'G', 'G', 'G', 'G']

# Pseudocode
```
CLASS Hidden Markov Model 
 
    CONSTRUCTOR(initial, transitions, emissions)
        derive states from the initial-probability keys
        derive alphabet from the emission-dictionary keys
        store the probabilities
        prepare their logarithms
 
METHOD viterbi(observations)
 
    IF observations is empty
        RETURN empty path, log probability 0
 
    IF any observation is outside the model's alphabet
        REPORT an invalid observation
 
    create score table, initially negative infinity
    create previous-state table, initially NONE
 
    INITIALIZATION
        FOR each state
            score[0][state] =
                log_initial[state]
                + log_emission[state][observations[0]]
 
    RECURSION
        FOR each position t after the first
            FOR each current state
                FOR each possible preceding state
                    candidate =
                        score[t - 1][preceding state]
                        + log_transition[preceding state][current state]
                        + log_emission[current state][observations[t]]
 
                    IF candidate is better than score[t][current state]
                        store candidate as the new score
                        store preceding state as the traceback pointer
 
    TERMINATION
        choose the state with the greatest score at the last position
        save that score as the best log probability
 
        IF that score is negative infinity
            REPORT that no valid path can produce the observations
 
    TRACEBACK
        put the chosen final state at the end of the path
        follow previous-state pointers backward
        RETURN the path and best log probability
```

# Notebook Usage
Import and download any modules required.
Run the code block by block, including the tests provided.

# Biological, Computational, Algorithmic Considerations 

**Biological** 
1. Determining the definition of each hidden state
   * Example: CpG island detection (CpG, Genome) 
2. Nucleotide or Amino Acid Sequence Properties
   * Considering GC-rich regions, conserved motifs 
3. Evolutionary Variation
   * Detecting mutations such as SNPs or indels

*Computational*
1. Memory Complexity and Runtime
   * Example: More than 2 states and a long sequence can create a large matrix and cause a slower runtime. 
2. Numerical Underflow
   * Using logarithmic functions to provide statistical significance 
3. Scalability
   * FASTA files are large and have many reads 

*Algorithmic* 
1. The number of states
   * Too few: missing biological data
   * Too many: overfitting 
2. Unknown nucleotides
   * 'N' is often seen in sequencing data, could we assign a small emission probabilities
3. Edge Cases

# Future Projects 
* *Use of several classes*: An important consideration is that this project will extend beyond the Viterbi algorithm. Using the idea of inheritance will be helpful as we add additional algorithms to HMMs. 
* *Use of decorators*: Although the usage of decorators is not necessary, using them in practice would provide insight into their function in object-oriented programming. Utilizing known and existing decorators such as ```@dataclass```, ```@setter```, or ```@getter``` can be useful in validation of data. 

# Successes
* *Output:* We were able to successfully produce an output for each of our methods within the class. Initially, we thought about creating one Viterbi method within the ```class Hidden Markov Model:```; however for testing purposes, we wanted to construct separate methods for each step (Initialization, Recursion, Termination). This allowed us to debug and test the code as we live-coded one by one together.   
* *Live-Coding Collaboration:* We were able to conduct a live-coding session where we could understand the code and methods of the Hidden Markov Model- Viterbi Algorithm. This facilitated our learning experiences to find gaps in our learning and work collaboratively to understand difficult concepts. 

# Struggles
* *Final Output:* The final output has a 'G' in index 2 (count using zero-based indexing) rather than a 'I', despite the max number of 'I' being greater than 'G'. A possible consideration is that the Viterbi algorithm takes the cumulative logarithmic traceback value, but we are still confused by what it means.
* *Jupyter Notebook:* A limit to the Jupyter notebook is not being able to separate the methods into separate code blocks for the class. We initially wanted to try and separate them for visualization and testing purposes, but there was a constraint in doing so. 


# Personal Reflections
## Group Leader
Group leader's reflection on the project


## Other member - Graziano
I would say that the biggest takeaway of this project was how we can improve together as a team. We set time to go through coding together and trying to understand the pseudocode and the mathematical reasoning behind it, those steps made our project stronger overall. I want to bring up few points that working as group made the resolution more clear. First to understand why the third position came out as “G” even though we had higher score at that point. We research and  concluded that the main goal is the optimal path and not only the not highest node point. That would made the understanding of how the table was working easier to be followed. And also how we as a team managed to build the project with the OOP in mind, specially for the next project, which will be useful to have those reusable pieces to be called into the project 8. Working as team for sure alleviate the burden a bit.

## Other member- Kailey
The concept of the Viterbi Algorithm within Hidden Markov Models made sense to me, but viewing the mathematical formulas and all of the various variables was a bit overwhelming initially. During lecture, it was noted that the variables will change based on the instructor and the method being taught, and that was true. A few Youtube videos and articles in, there was large variation within the variables, but the formulas and concepts remained the same.

Collaboration was a key factor on this project. Due to a few time constraints, we were not able to meet until Tuesday, but it ended up being the most productive. We shared our pseudocode and background information and took the time to live-code together. The concept of object-oriented programming is still new and complex to me, but I found this collaborative session to be useful. I gained insight into how classes work, how a constructor functions and how to effectively test each bit of code. The meeting was long, but very informative. Each person was able to understand the concept better without having to spend extra time working on it independently.

# Generative AI Appendix
Graziano:
Description of which generative AI was used and its version. NotebookLM 2.0 and Claude Opus 5
The entire prompt that was used to generate the content. Can you help me to fix my pseudocode to a the github format? Can you explain step by step how the Viterbi algorithm works mathematically, do not provide code samples or code output. I only want the reasoning behind the process.
An explanation of how it was used (e.g., to generate ideas). I used it as a tool to learn the concepts described on the articles and materials, asking for further clarification on the material and extra examples.
A justification for why generative AI was used. AI was used to bring a different explanation of the problem. It breaks down the process with simpler examples and guide was to understand the reasoning behind the formula.
