# LLaMA-Factory微调
安装项目的依赖包
```bash
pip install -e .
```
启动可视化终端微调
```bash
cd LLaMA-Factory
llamafactory-cli webui
```
# llama.cpp量化部署模型
编译CPP文件
基于CUDA
```bash
cd llama.cpp
cmake -B build_cuda -DLLAMA_CUDA=ON
cmake --build build_cuda --config Release -j 12
```

转化safetensors模型格式为gguf并量化为Q8_0
```bash
python convert-hf-to-gguf.py  /modelspath/xxx --outfile  /outmodel/modelname-q8_0-v1.gguf --outtype q8_0
```
终端运行gguf格式模型
```bash
cd llama.cpp/build_cuda/bin/
./llama-cli -m /modelpath/xxxx.gguf -cov
```
对gguf格式Q8_0模型再量化为Q4_1

```bash
cd llama.cpp/build_cuda/bin
./quantize --allow-requantize /modelspath/xxx-q8_0-v2_1.gguf /outmodelspath/xxx-q4_1-v1.gguf Q4_1
