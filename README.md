# Blog Generator with Llama 2

This project is a blog generator application built with Streamlit and powered by Meta's Llama 2 language model. The application generates blogs based on user input, supporting different styles of writing and allowing customization of the blog topic and word count.

## Features

- Generate blogs for specific job profiles such as Researchers, Data Scientists, or Common People.
- Specify a custom topic and desired word count.
- User-friendly interface built with Streamlit.
- Powered by the Llama 2 model from Meta.

---

## Prerequisites

1. **Python Environment**:

   - Python 3.7 or later.

2. **Dependencies**:
   Install the required Python libraries using the following command:

   ```bash
   pip install streamlit langchain ctransformers
   ```

3. **Llama 2 Model**:
   Download the Llama 2 model file `llama-2-7b-chat.ggmlv3.q8_0.bin` and place it in a `models/` directory at the root of the project. Ensure you comply with the Llama Community License.

---

## Usage Instructions

1. Clone this repository:

   ```bash
   git clone https://github.com/your-username/llama2-blog-generator.git
   cd llama2-blog-generator
   ```

2. Run the application:

   ```bash
   streamlit run app.py
   ```

3. Open the application in your browser at `http://localhost:8501`.

4. Enter the desired blog topic, word count, and writing style, and click "Generate" to create your blog.

---

## Code Overview

The main application code is structured as follows:

- **Model Initialization**: Uses the `CTransformers` library to load the Llama 2 model.
- **Prompt Template**: Dynamically generates prompts based on user inputs.
- **Streamlit Interface**: Provides a simple and intuitive UI for interacting with the model.

Example of the `getLLamaresponse` function:

```python
from langchain.prompts import PromptTemplate
from langchain.llms import CTransformers

# Function to get response from Llama 2 model
def getLLamaresponse(input_text, no_words, blog_style):
    llm = CTransformers(
        model='models/llama-2-7b-chat.ggmlv3.q8_0.bin',
        model_type='llama',
        config={'max_new_tokens': 256, 'temperature': 0.01}
    )
    template = """
        Write a blog for {blog_style} job profile for a topic {input_text}
        within {no_words} words.
    """
    prompt = PromptTemplate(
        input_variables=["blog_style", "input_text", "no_words"],
        template=template
    )
    response = llm(prompt.format(
        blog_style=blog_style, input_text=input_text, no_words=no_words
    ))
    print(response)
    return response
```

---

## Compliance with Llama 2 License

This project complies with the [Llama 2 Community License Agreement](https://github.com/meta-llama/llama/blob/main/LICENSE):

1. **Redistribution**:

   - The Llama 2 model binary is not distributed directly in this repository. Users must download it separately from Meta's official source.
   - This repository includes an attribution notice in this `README.md`.

2. **Usage Restrictions**:

   - The model outputs are not used to train or enhance other language models outside of Llama.
   - Users must agree to Meta's acceptable use policies, including not engaging in illegal, harmful, or deceptive activities.

3. **Attribution**:

   - This project uses the Llama 2 model licensed under the Llama 2 Community License. Copyright (c) Meta Platforms, Inc. All Rights Reserved.

4. **Commercial Usage**:
   - If your organization has over 700 million Monthly Active Users (MAUs), you must request a separate license from Meta.

---

## Disclaimer

This project is provided "as is" without any warranties, express or implied. The authors are not liable for any damages arising from its use.

---

## Contribution

Contributions are welcome! Please submit a pull request or open an issue to discuss improvements.

---

## License

This project is licensed under the Llama 2 Community License Agreement. Refer to [LICENSE](https://github.com/meta-llama/llama/blob/main/LICENSE) for more details.
