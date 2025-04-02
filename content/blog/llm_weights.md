+++
title = "What are LLM Weights?" 
date = "2025-03-15" 
+++

This is a **reference**, not a guide. 

In a modern LLM, the "weights" consist of several distinct collections of matrices and tensors that serve different functions during inference:

  1. Token Embeddings
    - Large matrix mapping token IDs to vector representations
    - Used at the very start of inference to convert input tokens to vectors
    - Typically shape: [vocab_size, hidden_dim]

  2. Attention Mechanism Weights
    - Query/Key/Value Projection Matrices:
        - In standard attention: 3 separate matrices [hidden_dim, hidden_dim]
      - In GQA: One Q matrix but fewer K/V matrices [hidden_dim, kv_dim]
      - Used to project hidden states into query, key, and value spaces
    - Output Projection Matrix:
        - Maps attention outputs back to hidden dimension [hidden_dim, hidden_dim]
      - Used after attention calculation to project back to main representation

  3. RoPE Parameters
    - Not traditional weight matrices but positional embedding tensors
    - Used to rotate query/key vectors to encode positional information
    - Applied during attention computation by complex multiplication

  4. Feedforward Network Weights
    - Up-projection Matrix: [hidden_dim, intermediate_dim]
        - Expands representation to larger dimension
    - Gate Matrix (for SwiGLU): [hidden_dim, intermediate_dim]
        - Controls information flow with element-wise multiplication
    - Down-projection Matrix: [intermediate_dim, hidden_dim]
        - Projects back to hidden dimension

  5. Layer Normalization Parameters
    - Scale/Gamma: [hidden_dim]
    - Bias/Beta: [hidden_dim]
    - Used before attention and FFN to normalize activations

  6. Output Weights
    - Final layer norm parameters
    - Projection to vocabulary (often tied to input embeddings)
    - Used to convert final hidden states to logits over vocabulary

  In inference, these weights are used in sequence:

  1. Input tokens → Embedding lookup → Initial vectors

  2. For each layer:
    - Normalize vectors → Layer norm weights
    - Project to Q/K/V → Attention projection matrices
    - Apply RoPE → Positional encoding parameters
    - Calculate attention (masked as needed)
    - Project back → Output projection matrix
    - Normalize → Layer norm weights
    - Pass through FFN → Up-projection, gate (SwiGLU), and down-projection matrices

  3. Final layer norm → Output projection → Logits

During inference, these matrices are applied sequentially as the input flows through the network. The KV cache optimization stores precomputed key and value tensors to avoid recomputing them for previously processed tokens.
