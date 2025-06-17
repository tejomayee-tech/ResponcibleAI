# Local AI for Python Coding


## How to Use AI for Python Code Generation:

**A. Using Ollama (Recommended for Ease):**

1.  **Install Ollama:** Download and install Ollama for your operating system from `ollama.com`.
2.  **Pull a Model:** Open your terminal and pull a code-focused model, for example:
    ```bash
    ollama pull codellama:python
    # Or for a more powerful general code model:
    ollama pull deepseek-coder:instruct
    ```
3.  **Interact via Python:**
    * **Direct Python Library:**
        ```python
        import ollama

        # Option 1: Simple chat
        response = ollama.chat(model='codellama:python', messages=[
          {'role': 'user', 'content': 'Generate a Python function to calculate the factorial of a number.'},
        ])
        print(response['message']['content'])

        # Option 2: Generate code based on a prompt
        response = ollama.generate(
            model='codellama:python',
            prompt='Write a Python class for a linked list with methods for insertion, deletion, and searching.'
        )
        print(response['response'])
        ```
    * **Via LangChain (for more complex applications):**
        ```python
        from langchain_community.llms import Ollama

        llm = Ollama(model="codellama:python")

        prompt = "Write a Python function to read a CSV file into a Pandas DataFrame and return the first 5 rows."
        print(llm.invoke(prompt))
        ```

**B. Using `llama.cpp-python` (for more control):**

1.  **Install `llama-cpp-python`:**
    ```bash
    pip install llama-cpp-python
    ```
    (Note: For GPU support, you might need to install with specific flags, e.g., `pip install llama-cpp-python --force-reinstall --no-cache-dir --verbose --config-settings cmake.define.LLAMA_CUBLAS=ON`)
2.  **Download a GGUF Model:** Go to Hugging Face and search for models in `GGUF` format, specifically "coder" or "instruct" models. TheBloke's repository is an excellent source.
    * Example: `TheBloke/CodeLlama-7B-Instruct-GGUF`
3.  **Interact via Python:**
    ```python
    from llama_cpp import Llama

    # Replace with the actual path to your downloaded GGUF model file
    model_path = "./path/to/your/codellama-7b-instruct.Q4_K_M.gguf"

    # Initialize the LLM
    # n_ctx: context window size, adjust based on your needs and VRAM
    # n_gpu_layers: number of layers to offload to GPU (-1 for all, 0 for none)
    llm = Llama(
        model_path=model_path,
        n_ctx=4096,  # Adjust context window as needed
        n_gpu_layers=-1, # Or a specific number if you have a GPU
        verbose=False
    )

    prompt = "Write a Python function that takes a list of numbers and returns a new list with only the even numbers."

    # For instruction-tuned models, it's often best to use a chat-like format
    messages = [
        {"role": "system", "content": "You are an expert Python programmer."},
        {"role": "user", "content": prompt}
    ]

    output = llm.create_chat_completion(messages=messages, temperature=0.7, max_tokens=500)
    print(output["choices"][0]["message"]["content"])
    ```

**Important Considerations for Local LLMs:**

* **Hardware:**
    * **RAM:** Crucial for loading the model weights. Larger models (e.g., 30B+ parameters) will require 32GB+ of RAM. Quantized models (e.g., Q4_K_M) are smaller but have slightly reduced performance.
    * **GPU (VRAM):** A dedicated GPU with ample VRAM (e.g., 8GB, 12GB, 24GB+) significantly speeds up inference. The more VRAM, the larger the model you can run on the GPU. Even a modest GPU can provide a noticeable boost.
    * **CPU:** Important if you don't have enough VRAM to offload all layers to the GPU, as the CPU will handle the remaining layers.
* **Model Quantization:** Models are often available in "quantized" versions (e.g., Q4\_K\_M, Q5\_K\_S). These are smaller and run faster but might have a slight drop in quality compared to their full-precision counterparts.
* **Prompt Engineering:** Even with powerful local LLMs, the quality of your prompt heavily influences the quality of the generated code. Be clear, specific, and provide examples if possible.
* **Temperature & Top-P:** These parameters control the creativity and randomness of the output. Experiment with them:
    * **Temperature:** Higher values (e.g., 0.7-0.9) lead to more diverse/creative output. Lower values (e.g., 0.1-0.3) lead to more deterministic/focused output. For code, you often want lower temperatures for correctness.
    * **Top-P:** Another way to control diversity.
* **Context Window (`n_ctx`):** This defines how much "memory" the LLM has. A larger context window allows the model to consider more of your existing code or previous interactions, which is vital for complex code generation. However, it consumes more RAM/VRAM.

By combining these tools and models, you can set up a powerful local LLM environment for all your Python coding needs!
