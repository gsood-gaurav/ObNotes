![[Pasted image 20240301115042.png]]
![[Pasted image 20240301115017.png]]
- Memorization is a Poisson Point Process
- 300B tokens
- GPT-NeoX tokenizer.
- The deduplicated Pile only contains 207B tokens, so we run for ≈1.5 epochs on it.
A100s with 40GB of memory
![[Pasted image 20240301115645.png]]
![[Pasted image 20240301115625.png]]

![[Pasted image 20240301115748.png]]
![[Pasted image 20240301115909.png]]
Consequently, we use a batch size of 1024 samples with a
sequence length of 2048 (2,097,152 tokens) for all models