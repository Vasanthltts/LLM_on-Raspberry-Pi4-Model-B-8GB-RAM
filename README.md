# LLM_on-Raspberry-Pi4-Model-B-8GB-RAM

Here is my step-by-step guide to running Large Language Models (LLMs) using llama.cpp on a Raspberry Pi. 

# Description

Here we are going to use Llama.cpp
The main goal of llama.cpp is to enable LLM inference with minimal setup and state-of-the-art performance on a wide variety of hardware - locally and in the cloud.

1) Plain C/C++ implementation without any dependencies.

2)  Apple silicon is a first-class citizen - optimized via ARM NEON, Accelerate and Metal frameworks.

3) AVX, AVX2 and AVX512 support for x86 architectures.

4) 1.5-bit, 2-bit, 3-bit, 4-bit, 5-bit, 6-bit, and 8-bit integer quantization for faster inference and reduced memory use.

5) Custom CUDA kernels for running LLMs on NVIDIA GPUs (support for AMD GPUs via HIP).

6) Vulkan and SYCL backend support.

7) CPU+GPU hybrid inference to partially accelerate models larger than the total VRAM capacity.

Since its inception, the project has improved significantly thanks to many contributions. It is the main playground for developing new features for the ggml library.

# Links

1) https://github.com/ggerganov/llama.cpp

Here I have Taken Medical LLM Apollo 2B model, Microsoft/Phi-2, Google/Gemma-2B amd Quantized that model using Intel Open Vino Framework.

If you are not interesting in Quantization of the LLM model you can just visit the below hugging Face website where You can downlaod the Quantized model with all types of integer quantization in gguf format.

2) https://huggingface.co/RichardErkhov/FreedomIntelligence_-_Apollo-2B-gguf
3) https://huggingface.co/ggerganov/gemma-2b-Q8_0-GGUF/tree/main
4) https://huggingface.co/TheBloke/phi-2-GGUF/tree/main

# Prepare development environment

     sudo apt update
     sudo apt install git g++ wget build-essential

# Download and compile llama.cpp

    git clone https://github.com/ggerganov/llama.cpp.git
    cd llama.cpp
    make -j
This make command will take some time to run ~ 20mins.

# Download the LLM 

You now need to download a language model. Pick one of the model below or download the model of your choice. Make sure you download the GGUF version (not the GGML variant).
These model files are several Gigabytes each, so make sure you have enough free space. If your SD Card is doesn't have the space you can try using some external storage, even a USB flash drive.

You can check the free space on the drive which holds your home directory using 
     df -h ~

# Download Apollo-2B.Q8_0.gguf
        
          cd models
          ./llama-cli -m <path_to_your_model>Apollo-2B.Q8_0.gguf -p "Give  5 simple steps to cure cough:\nStep 1:" -n 400 -e

Output:

          Give  5 simple steps to cure cough:
          Step 1: Identify the cause of cough.
          Step 2: Look for any allergy symptoms.
          Step 3: Drink plenty of fluids.
          Step 4: Treat the underlying cause of the cough.
          Step 5: Use an expectorant.
 
          1. Identify the cause of cough.
          The first step is to identify the cause of your cough. It could be due to allergies, respiratory infections, or even an underlying medical condition such as asthma or chronic bronchitis. By understanding the cause, you can target your treatment more effectively.
 
          2. Look for any allergy symptoms.
          If your cough is caused by an allergy, it's important to identify the specific allergen that's triggering your symptoms. This can help you avoid the allergen in the future and prevent your cough from recurring.
 
          3. Drink plenty of fluids.
          Staying hydrated can help thin out mucus and make it easier to expel from your body. Aim to drink at least eight glasses of water a day.
 
          4. Treat the underlying cause of the cough.
          If your cough is due to an infection, it's important to treat the underlying cause. If it's a cold or flu, over-the-counter medications can help alleviate symptoms. If it's asthma or chronic bronchitis, you may need to work with a healthcare provider to manage your condition.
 
          5. Use an expectorant.
          There are several over-the-counter expectorants available that can help thin out mucus and make it easier to cough up. These can be particularly useful if your cough is accompanied by a productive cough.
 
          Remember, if your cough persists or worsens, or if you have any other concerning symptoms, it's important to consult with a healthcare provider for further evaluation and treatment. [end of text]
 
          llama_print_timings:        load time =  119416.46 ms
          llama_print_timings:      sample time =     421.03 ms /   361 runs   (    1.17 ms per token,   857.43 tokens per second)
          llama_print_timings: prompt eval time =    4064.45 ms /    15 tokens (  270.96 ms per token,     3.69 tokens per second)
          llama_print_timings:        eval time =  411001.43 ms /   360 runs   ( 1141.67 ms per token,     0.88 tokens per second)
          llama_print_timings:       total time =  416335.21 ms /   375 tokens
          Log end

# Gemma-2B_Q_8

    ./llama-cli -m /home/vasanth/llama.cpp/models/gemma-2b.Q8_0.gguf -p "Who is the goat of cricket?" -n 400 -e

Output

    Who is the goat of cricket? In the history of cricket, there have been several players who have been termed as the goat or the goat of the game. These players have made a place in the hearts of the fans and cricketers themselves with their  exceptional talent and performance. In this article, we will be taking a look at the players who have been referred to as the goat in cricket.
 
    <h2><strong>Who is the Goat of Cricket?</strong></h2>
 
    These players have shown their talent in various formats of cricket and have made a name for themselves. The list includes names such as Sachin Tendulkar, <strong>Ricky Ponting</strong>, Brian Lara, <strong>Jacques Kallis</strong>, and many others. These players have been referred to as the goat because of their exceptional performances and contributions to the game.
 
    <h3><strong>Here is the list of the Goat of Cricket:</strong></h3>
 
    <strong>Sachin Tendulkar:</strong> Sachin Tendulkar is considered one of the greatest batsmen in the history of cricket. He holds the record for the most runs scored in ODIs (20,000) and Test Matches (15,921). He was known for his aggressive batting style and was called the “Master Blaster”.
 
    <strong>Ricky Ponting:</strong> Ricky Ponting was known for his consistent performances in international cricket. He led the Australian cricket team to many victories, including the 2003 Ashes series and the 2007 World Cup. He was also a master of the short game and was often referred to as the “Hitman”.
 
    <strong>Brian Lara:</strong> Brian Lara was known for his big-hitting and was considered one of the greatest batsmen of all time. He was known for his ability to score big runs in limited overs cricket and was often referred to as the “Prince of Port of Spain”.
 
    <strong>Jacques Kallis:</strong> Jacques Kallis was known for his all-round abilities and was a master of many formats of cricket. He was
    llama_print_timings:        load time =   61407.98 ms
    llama_print_timings:      sample time =     437.38 ms /   400 runs   (    1.09 ms per token,   914.54 tokens per second)
    llama_print_timings: prompt eval time =    2645.35 ms /     8 tokens (  330.67 ms per token,     3.02 tokens per second)
    llama_print_timings:        eval time =  439807.18 ms /   399 runs   ( 1102.27 ms per token,     0.91 tokens per second)
    llama_print_timings:       total time =  443802.27 ms /   407 tokens
    Log end

# phi-2.Q5

    ./llama-cli -m /home/vasanth/llama.cpp/models/phi-2.Q5_K_M.gguf -p "Write a python code in fibonacci series?" -n 400 -e

Output

    Write a python code in fibonacci series?
 
    def fibonacci(n):
    if n <= 0:
        print("Incorrect input")
    elif n == 1:
        return 0
    elif n == 2:
        return 1
    else:
        return(fibonacci(n-1) + fibonacci(n-2))
 
    n = int(input("Enter number : "))
    print(fibonacci(n))
 
    A:
 
    There is a way to print out the result of the fibonacci function
    fibonacci(n):
    if n<0:
        print("Incorrect input")
    elif n==1:
        return 0
    elif n==2:
        return 1
    else:
        return(fibonacci(n-1)+fibonacci(n-2))
    n = int(input("Enter number : "))
    print(fibonacci(n))
 
    A:
 
    The problem is that you are trying to print the return value of your function.  Return statements are used to return values from functions.
    To print the result of the function call, you have to print the value returned.
    def fib(n):
    if n <= 0:
        return False
    if n == 1:
        return 0
    if n == 2:
        return 1
    return(fib(n-1) + fib(n-2))
 
    n = int(input("Enter number : "))
    print(fib(n))
 
    A:
 
    If you want to print the result you can simply use
    print(fibonacci(n))
 
    [end of text]
 
    llama_print_timings:        load time =   48560.13 ms
    llama_print_timings:      sample time =     139.99 ms /   371 runs   (    0.38 ms per token,  2650.15 tokens per second)
    llama_print_timings: prompt eval time =    2880.57 ms /    10 tokens (  288.06 ms per token,     3.47 tokens per second)
    llama_print_timings:        eval time =  349539.15 ms /   370 runs   (  944.70 ms per token,     1.06 tokens per second)
    llama_print_timings:       total time =  352918.36 ms /   380 tokens
    Log end


# Conversation mode
If you want a more ChatGPT-like experience, you can run in conversation mode by passing -cnv as a parameter:

    llama-cli -m your_model.gguf -p "You are a helpful assistant" -cnv
    Output:

    > hi, who are you?
    Hi there! I'm your helpful assistant! I'm an AI-powered chatbot designed to assist and provide information to users like you. I'm here to help answer your questions, provide guidance, and offer support on a wide range of topics. I'm a friendly and knowledgeable AI, and I'm always happy to help with anything you need. What's on your mind, and how can I assist you today?

    > what is 1+1?
    Easy peasy! The answer to 1+1 is... 2!
    

# Performance

1) Model Size vs. Speed: Smaller models (like Apollo-2B.Q5_0) can often be faster at token generation, especially for tasks that don't require the full capacity of a larger model.

2) Prompt Evaluation: Both models have similar prompt evaluation speeds, indicating that this operation might be less sensitive to model size.

3) Efficiency: The smaller model (Apollo-2B.Q5_0) demonstrates higher overall efficiency, suggesting it might be better suited for certain applications where speed is a priority.

# Additional Considerations

1) Hardware: The underlying hardware (CPU, GPU) can significantly impact performance.
2) Task Complexity: The specific task being performed can influence token generation speed.
3) Quantization: Using lower bit depths (like 5-bit) can trade off accuracy for speed.
