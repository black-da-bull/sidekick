FROM python:3.10-slim

COPY symspell /code/symspell

WORKDIR /code

# Install build/dev tools
RUN apt-get update \
&& apt-get install gcc curl git g++ -y \
&& apt-get clean

# Install Rust
RUN curl https://sh.rustup.rs -sSf | bash -s -- -y

# Install Python requirements
RUN pip install numpy scipy cython scikit-learn setuptools-rust
RUN PATH="$HOME/.cargo/bin:$PATH" pip install -e ./symspell/bindings/Python
RUN pip install -e git://github.com/facebookresearch/fastText.git#egg=fasttext

COPY preprocess.py /code/preprocess.py
CMD python preprocess.py
